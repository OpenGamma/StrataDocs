---
title: Adding a New Measure
permalink: /add_measure/
---

In Strata, measures define the values that can be calculated for a trade or other calculation target.
For example, Strata provides a standard set of measures including present value and PV01 (see the
[`Measures`]({{site.baseurl}}/apidocs/com/opengamma/strata/measure/Measures.html) class).
When a user requests a calculation they specify the measures that should be calculated and the rules defining
how they should be calculated.

The set of measures calculated by Strata is extensible.
Users can add new measures for the built-in asset classes and can also add support for the built-in measures
for new asset classes.

## Calculation Functions

Measures are calculated by implementations of
[`DerivedCalculationFunction`]({{site.baseurl}}/apidocs/com/opengamma/strata/calc/runner/DerivedCalculationFunction.html) or
[`CalculationFunction`]({{site.baseurl}}/apidocs/com/opengamma/strata/calc/runner/CalculationFunction.html).
`DerivedCalculationFunction` is used when adding new measures for an asset class already exists in Strata.
`CalculationFunction` is used when adding an asset class that does not already exist in Strata.

Adding a new measure to Strata requires three steps:

* Create a `Measure` instance to identify the measure and 
* Create a function to calculate the measure
* Provide pricing rules linking the `Measure` to the function

## Integrating the new function

The new function is normally integrated with the existing ones:

```java
CalculationFunctions combined = StandardComponents.calculationFunctions().composedWith(myNewFunction);
```

The combined instance is then passed in via `CalculationRules`.


## The DerivedCalculationFunction Interface

The interface `DerivedCalculationFunction` is implemented to calculate one additional measures for an asset class.
It works by first calculating a base set of measures, then calculating the derived measure.
In most cases you should extend `AbstractDerivedCalculationFunction` which only has one abstract method - `calculate()`.

`DerivedCalculationFunction` itself has five methods:

```java
public interface DerivedCalculationFunction<T extends CalculationTarget, R> {

  public abstract Class<T> targetType();

  public abstract Measure measure();

  public abstract Set<Measure> requiredMeasures();

  public abstract FunctionRequirements requirements(T target, CalculationParameters parameters, ReferenceData refData);

  public abstract R calculate(
      T target,
      Map<Measure, Object> requiredMeasures,
      CalculationParameters parameters,
      ScenarioMarketData marketData,
      ReferenceData refData);
}
```

### Target type

The `targetType()` method specifies the target type, such as `ResolvedSwap.class`.
Each derived function implementation handles one type of target.

### Measure

The `measure()` method specifies which measure is supported.
Each derived function implementation handles the calculation of one measure.

### Required measures

The `requiredMeasures()` method specifies which measures the derived function depends on.
Normally this include the resolved target - `Measures.RESOLVED_TARGET`.

### Requirements

The `requirements()` method provides the ability to determine the market data needed
for the combination of the trade and measure. This can be used to validate that the
market data is available before pricing, or to drive the process of creating the market data.
More details can be found [here]({{site.baseurl}}/market_data/).

### Calculate

The `calculate()` method is where the main calculation is performed.
It receives the target and the map of measures that the calculation depends on.
See below for more information about how `calculate()` should be implemented.


## The CalculationFunction Interface

The interface `CalculationFunction` is implemented to calculate values for measures,
but only one can be registered for each asset class.
It contains four methods:

```java
public interface CalculationFunction<T extends CalculationTarget> {

  Class<T> targetType();

  Set<Measure> supportedMeasures();

  Currency naturalCurrency(T target, ReferenceData refData);

  FunctionRequirements requirements(
      T target, Set<Measure> measures, CalculationParameters parameters, ReferenceData refData);

  Map<Measure, Result<?>> calculate(
      T target,
      Set<Measure> measures,
      CalculationParameters parameters,
      ScenarioMarketData marketData,
      ReferenceData refData);

}
```

### Target type

The `targetType()` method specifies the target type, such as `ResolvedSwap.class`.
Each derived function implementation handles one type of target.

### Supported measures

The `supportedMeasures()` method specifies which measures are supported.
Each function implementation will handle one or more measures.

### Natural currency

The `naturalCurrency()` method provides the "natural" currency of the specified target.

For single-currency trades, the "natural" currency is the currency of the trade.

For cross-currency trades, the choice of "natural" currency is more arbitrary.
It may be currency of the fixed leg, the currency of the first leg, the base
currency in terms of the standard market ordering, or anything other choice that is consistent.


### Requirements

The `requirements()` method provides the ability to determine the market data needed
for the combination of the trade and measures. This can be used to validate that the
market data is available before pricing, or to drive the process of creating the market data.
More details can be found [here]({{site.baseurl}}/market_data/).

#### Function requirements

The `requirements` method has a parameter for the calculation target and returns an instance of `FunctionRequirements`.
The requirements specify the market data required by the function to calculate a value for the target.

Market data is identified by implementations of `MarketDataId`.
The function creates a market data identifier for each piece of market data it requires and populates the
`FunctionRequirements`. The requirements contain three types of values:

* Single values, for example a curve or a quoted price
* Time series of quoted values
* Output currencies

##### Single Market Data Values

Single market data values are individual items are market data used in the calculations, and they can be of any type.
A their simplest they might be a `double` value representing a quoted price or rate.
They can also be complex values derived from underlying data, for example a curve.

Single market data values can be values that are directly observable in the market, for example rates or prices,
or they can be derived from other underlying market data, for example calibrated curves or volatility surfaces.

##### Time Series

Time series contain multiple values of an item of observable market data over a ranges of dates.
For example, a series of index rates used for historical fixings.

The values in a time series are always of type `double`.

##### Output Currencies

The Strata calculation runner is able to automatically convert currency values into different currencies for
the purposes of reporting. In order to perform this conversion the required FX rates must be available in the market data. 

The calculation runner must know which currencies are included in the results in order to provide the correct FX rates.
Therefore if the result of the function includes any currency value, the currencies should be included in
the set of output currencies.

#### Example requirements Implementation

The code below shows an example of a `requirements` method taken from the Strata class `FraCalculationFunction`.
It demonstrates how to create a set of `FunctionRequirements` for the data required to calculate the price of a FRA.

A FRA references one or two indices and one currency. In order to calculate the price of a FRA the
following market data is required:

* A time series of historical rates for each of the indices
* A forward curve for predicting the future values of the rates for each of the indices
* A discount curve for the currency used for discounting future values

The requirements method must be implemented to return these items in the `FunctionRequirements`.
In most case, the function will use an instance of `CalculationParameters`.
The `requirements` method will delegate most of the implementation to the parameters instance.


### Calculate

The `calculate()` method calculates a value for each of the specified measures for the calculation target (normally a trade).
The method parameters are the calculation target, measures and an instance of `ScenarioMarketData` containing
the market data required for the calculation.

To perform efficient calculations, the interface is designed to handle multiple measures and multiple scenarios efficiently.
In order to achieve this, the `calculate` method is expected to calculate multiple values.
This may allow functions to avoid repeating common calculations when a value is calculated for the
same target across multiple scenarios and measures.

In simple cases, or when integrating with existing calculation libraries, the underlying calculations are
likely to produce one value at a time. In fact the default pricers included with Strata behave this way.
In this case it is the job of the `calculate` method to unpack the scenario market data, call the underlying
calculations repeatedly and pack the results into a single return value.

#### Looking up Market Data

A function requests market data by calling the following methods on `ScenarioMarketData`:

* `getValue`
* `getTimeSeries`

The single argument to these methods is the market data key identifying the market data required.
The return value of `getTimeSeries` is a `LocalDateDoubleTimeSeries`. The return value of `getValue`
is a `MarketDataBox` which provides a market data value for each scenario. The market data value for
each scenario is provided by `MarketDataBox.getValue(int scenarioIndex)`.

If the market data doesn't contain a value for the key an exception will be thrown.
The exception will be caught by the calculation runner and the results will contain an error
explaining the calculation failed because the market data was not available.

#### Return Values

As explained above, the `calculate` method performs calculations for all scenarios at once.
The calculated values can be divided into two categories:

* Aggregate values, for example the average, maximum or minimum value across all scenarios.
* Individual values, one for each scenario. 

If the calculation produces an aggregate value there is are no restrictions on the return type of `calculate`.

If the calculation produces a value for each scenario the calculate method should return an implementation of
`ScenarioResult`. This allows the calculation engine to handle the results more intelligently in the
common case of running a single scenario.

If the calculated value contains currency amounts the return value should implement `CurrencyConvertible`.
Convertible values can be automatically converted to the reporting currency.

### Function Design Guidelines

The Strata calculation engines performs calculations in parallel so it is possible a function will be executed
concurrently on multiple threads with different targets. Therefore functions implementations must be thread safe.

It is strongly recommended that functions should be completely stateless, receiving everything required to
perform the calculation via method arguments. This not only ensures they are thread safe but makes it
immediately obvious they are safe.

If a function needs to store any configuration parameters as fields, the fields should be final
and the configuration objects should be immutable.
