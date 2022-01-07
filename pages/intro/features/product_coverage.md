---
title: Product Coverage
permalink: /product_coverage/
---

Strata includes the following coverage:

<div class="product-coverage">
<table>
  <thead>
    <tr>
      <th>Asset class</th>
      <th>Pricer <a id="pricer" href="#pricer-footnote"><sup>1</sup></a></th>
      <th>Calc API <a id="calcapi" href="#calcapi-footnote"><sup>2</sup></a></th>
      <th>Examples <a id="examples" href="#examples-footnote"><sup>3</sup></a></th>
      <th>Load from FpML</th>
      <th>Load from CSV</th>
    </tr>
  </thead>
  <tbody>
  <tr>
    <td><a href="{{site.baseurl}}/swap">Swap</a><br />
      <span class="note">Including Vanilla, OIS, Basis, Cross Currency, Variable Notional and Inflation</span></td>
    <td><i class="fa fa-check"></i></td>
    <td><i class="fa fa-check"></i></td>
    <td><i class="fa fa-check"></i></td>
    <td><i class="fa fa-check"></i></td>
    <td><i class="fa fa-check"></i></td>
  </tr>
  <tr>
    <td><a href="{{site.baseurl}}/fra">FRA</a></td>
    <td><i class="fa fa-check"></i></td>
    <td><i class="fa fa-check"></i></td>
    <td><i class="fa fa-check"></i></td>
    <td><i class="fa fa-check"></i></td>
    <td><i class="fa fa-check"></i></td>
  </tr>
  <tr>
    <td><a href="{{site.baseurl}}/fx_single">FX Forward/Spot</a></td>
    <td><i class="fa fa-check"></i></td>
    <td><i class="fa fa-check"></i></td>
    <td><i class="fa fa-check"></i></td>
    <td><i class="fa fa-check"></i></td>
    <td><i class="fa fa-check"></i></td>
  </tr>
  <tr>
    <td>FX NDF</td>
    <td><i class="fa fa-check"></i></td>
    <td><i class="fa fa-check"></i></td>
    <td><i class="fa fa-check"></i></td>
    <td><i class="fa fa-check"></i></td>
    <td></td>
  </tr>
  <tr>
    <td><a href="{{site.baseurl}}/fx_swap">FX Swap</a></td>
    <td><i class="fa fa-check"></i></td>
    <td><i class="fa fa-check"></i></td>
    <td><i class="fa fa-check"></i></td>
    <td><i class="fa fa-check"></i></td>
    <td><i class="fa fa-check"></i></td>
  </tr>
  <tr>
    <td>STIR Future (Ibor)</td>
    <td><i class="fa fa-check"></i></td>
    <td><i class="fa fa-check"></i></td>
    <td><i class="fa fa-check"></i></td>
    <td class="na"></td>
    <td><i class="fa fa-check"></i><a id="securitycsv" href="#securitycsv-footnote"><sup>4</sup></a></td>
  </tr>
  <tr>
    <td>STIR Future Option</td>
    <td><i class="fa fa-check"></i><br />
      <span class="note">Normal</span></td>
    <td><i class="fa fa-check"></i></td>
    <td></td>
    <td class="na"></td>
    <td><i class="fa fa-check"></i><a id="securitycsv" href="#securitycsv-footnote"><sup>4</sup></a></td>
  </tr>
  <tr>
    <td>STIR Future (Overnight)</td>
    <td><i class="fa fa-check"></i></td>
    <td><i class="fa fa-check"></i></td>
    <td></td>
    <td class="na"></td>
    <td><i class="fa fa-check"></i><a id="securitycsv" href="#securitycsv-footnote"><sup>4</sup></a></td>
  </tr>
  <tr>
    <td>Deliverable Swap Future</td>
    <td><i class="fa fa-check"></i></td>
    <td><i class="fa fa-check"></i></td>
    <td><i class="fa fa-check"></i></td>
    <td class="na"></td>
    <td><i class="fa fa-check"></i><a id="securitycsv" href="#securitycsv-footnote"><sup>4</sup></a></td>
  </tr>
  <tr>
    <td><a href="{{site.baseurl}}/term_deposit">Term Deposit</a></td>
    <td><i class="fa fa-check"></i></td>
    <td><i class="fa fa-check"></i></td>
    <td><i class="fa fa-check"></i></td>
    <td><i class="fa fa-check"></i></td>
    <td><i class="fa fa-check"></i></td>
  </tr>
  <tr>
    <td><a href="{{site.baseurl}}/bullet_payment">Bullet Payment</a></td>
    <td><i class="fa fa-check"></i></td>
    <td><i class="fa fa-check"></i></td>
    <td><i class="fa fa-check"></i></td>
    <td><i class="fa fa-check"></i></td>
    <td><i class="fa fa-check"></i></td>
  </tr>
  <tr>
    <td><a href="{{site.baseurl}}/swaption">Swaption</a><br />
      <span class="note">Including physical and cash-settled</span></td>
    <td><i class="fa fa-check"></i><br />
      <span class="note">Normal, Black, SABR</span></td>
    <td><i class="fa fa-check"></i></td>
    <td></td>
    <td><i class="fa fa-check"></i></td>
    <td><i class="fa fa-check"></i></td>
  </tr>
  <tr>
    <td>Bill</td>
    <td><i class="fa fa-check"></i></td>
    <td><i class="fa fa-check"></i></td>
    <td></td>
    <td class="na"></td>
    <td><i class="fa fa-check"></i><a id="securitycsv" href="#securitycsv-footnote"><sup>4</sup></a></td>
  </tr>
  <tr>
    <td>Fixed-Coupon Bond</td>
    <td><i class="fa fa-check"></i></td>
    <td><i class="fa fa-check"></i></td>
    <td></td>
    <td class="na"></td>
    <td><i class="fa fa-check"></i><a id="securitycsv" href="#securitycsv-footnote"><sup>4</sup></a></td>
  </tr>
  <tr>
    <td>Capital Indexed Bond<br />
      <span class="note">Including support for US TIPS</span></td>
    <td><i class="fa fa-check"></i></td>
    <td><i class="fa fa-check"></i></td>
    <td></td>
    <td class="na"></td>
    <td><i class="fa fa-check"></i><a id="securitycsv" href="#securitycsv-footnote"><sup>4</sup></a></td>
  </tr>
  <tr>
    <td>Bond Future</td>
    <td><i class="fa fa-check"></i></td>
    <td><i class="fa fa-check"></i></td>
    <td></td>
    <td class="na"></td>
    <td><i class="fa fa-check"></i><a id="securitycsv" href="#securitycsv-footnote"><sup>4</sup></a></td>
  </tr>
  <tr>
    <td>Bond Future Option</td>
    <td><i class="fa fa-check"></i><br />
      <span class="note">Black</span></td>
    <td><i class="fa fa-check"></i></td>
    <td></td>
    <td class="na"></td>
    <td><i class="fa fa-check"></i><a id="securitycsv" href="#securitycsv-footnote"><sup>4</sup></a></td>
  </tr>
  <tr>
    <td><a href="{{site.baseurl}}/fx_vanilla_option">FX Vanilla Option</a></td>
    <td><i class="fa fa-check"></i><br />
      <span class="note">Black, Vanna Volga</span></td>
    <td><i class="fa fa-check"></i></td>
    <td></td>
    <td></td>
    <td><i class="fa fa-check"></i></td>
  </tr>
  <tr>
    <td>FX Single Barrier Option</td>
    <td><i class="fa fa-check"></i><br />
      <span class="note">Black, Trinomial tree</span></td>
    <td><i class="fa fa-check"></i></td>
    <td></td>
    <td></td>
    <td><i class="fa fa-check"></i></td>
  </tr>
  <tr>
    <td>CMS<br />
    <span class="note">Including cap/floor</span></td>
    <td><i class="fa fa-check"></i><br />
      <span class="note">SABR</span></td>
    <td><i class="fa fa-check"></i></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>Ibor cap/floor</td>
    <td><i class="fa fa-check"></i><br />
      <span class="note">Normal, Black</span></td>
    <td><i class="fa fa-check"></i></td>
    <td></td>
    <td></td>
    <td><i class="fa fa-check"></i></td>
  </tr>
  <tr>
    <td><a href="{{site.baseurl}}/cds">CDS</a><br />
      <span class="note">Including Single Name and Index</span></td>
    <td><i class="fa fa-check"></i></td>
    <td><i class="fa fa-check"></i></td>
    <td></td>
    <td><i class="fa fa-check"></i></td>
    <td><i class="fa fa-check"></i></td>
  </tr>
  <tr>
    <td>Generic Security</td>
    <td class="na">MtM</td>
    <td><i class="fa fa-check"></i></td>
    <td><i class="fa fa-check"></i></td>
    <td class="na"></td>
    <td><i class="fa fa-check"></i><a id="securitycsv" href="#securitycsv-footnote"><sup>4</sup></a></td>
  </tr>
  </tbody>
</table>
</div>

<a id="pricer-footnote" href="#pricer"><sup>1</sup></a>
Pricer support means Strata includes one or more model implementations which provide pricing and risk calculations.
These provide an API which, given the required market data, calculates a particular measure.
For details on the specific calculations supported, please see the relevant asset class page.

<a id="calcapi-footnote" href="#calcapi"><sup>2</sup></a>
The Calculation API allows measures to be calculated on mixed portfolios in a single operation, automatically
calling the appropriate pricer, and returning a table of results. It also includes scenario capabilities.
Support for the Calculation API means that the pricer is fully integrated using Strata's standard measure names.
This also implies support in the measure-level API

<a id="examples-footnote" href="#examples"><sup>3</sup></a>
Code examples are included in the strata-examples module.
This also indicates that the command-line tool includes an example portfolio and report for the asset class.

<a id="securitycsv-footnote" href="#securitycsv"><sup>4</sup></a>
CSV loader for securities refers to the security identifier, with the security details
expected to be available in reference data.


## Curve calibration

Strata includes a full implementation of the multi-curve framework for curve calibration.
The following asset classes can be used when defining curves:

* Ibor Fixing
* Term Deposit
* FRA
* STIR Future (Ibor)
* Vanilla Swap (Fixed vs Ibor)
* OIS (Fixed vs Overnight)
* Basis Swap (Ibor vs Ibor and Overnight vs Ibor)
* Three Leg Basis Swap (Euribor)
* Cross-currency Swap (Ibor vs Ibor)
* Inflation Swap (Fixed vs Inflation)
* Ibor/Overnight Future
* FX Swap
