<template>
  <div style="background-color: #def2f1;font-variant: small-caps;">
    <b-container class="bv-example-row">
      <b-row>
        <b-col cols="12">
          <div class="text-center">
            <div class='p-4 segment card'>
              <h1 class="heading" ><b>QR Client Application</b></h1>
            </div>
          </div>
        </b-col>
      </b-row>
      <b-row>
        <b-col cols="12">
          <span style="display: block;">
            <b-form-textarea style="text-align: left;background: transparent; color:red; border:none"
                          v-model="response.status"
                          readonly
                          no-resize></b-form-textarea>
          </span>
        </b-col>
      </b-row>
      <b-row>
        <b-col sm="12" md="12" lg="8" xl="8">
          <b-form @reset="onReset" v-if="show" class="form-horizontal">
            <div class='p-4 segment card'>
              <h4 class="heading"><b>Creditor</b></h4>
              <b-form-group>
                <b-input-group size="sm" prepend="Name:" id="creditorNameLabel"
                               label-for="creditorName">
                  <b-form-input size="sm" id="creditorNameInput"
                                type="text"
                                v-model="body.creditorInformation.creditor.name"
                                name="Creditor Name"
                                v-validate="'required|min:1|max:70'"
                                required>
                  </b-form-input>
                  <b-input-group-append>
                    <b-button
                      variant="secondary"
                      v-b-tooltip.hover title="The creditor’s name or company according to the account name
                       Maximum 70 characters permitted
                       First name (optional, if available) + last name or company name">?
                    </b-button>
                  </b-input-group-append>
                  <br/>
                  <i v-show="errors.has('Creditor Name')" class="fa fa-warning"></i>
                  <span v-show="errors.has('Creditor Name')" style="color: red" class="help is-danger">{{ errors.first('Creditor Name') }}</span>
                </b-input-group>
              </b-form-group>
              <b-form-group>
                <b-input-group size="sm" prepend="Street:" id="creditorStreetLabel"
                               label-for="creditorStreet">
                  <b-form-input size="sm" id="creditorStreetInput"
                                type="text"
                                name="Creditor Street"
                                v-model="body.creditorInformation.creditor.streetName"
                                v-validate="'min:1|max:70'">
                  </b-form-input>
                  <b-input-group-append>
                    <b-button
                      variant="secondary"
                      v-b-tooltip.hover title="Street/P.O. box of the creditor
                       Maximum 70 characters permitted, may not include any house or building number.">?
                    </b-button>
                  </b-input-group-append>
                  <br/>
                  <i v-show="errors.has('Creditor Street')" class="fa fa-warning"></i>
                  <span v-show="errors.has('Creditor Street')" style="color: red" class="help is-danger">{{ errors.first('Creditor Street') }}</span>
                </b-input-group>
              </b-form-group>
              <b-form-group>
                <b-input-group size="sm" prepend="House Number:" id="creditorHouseNumberLabel"
                               label-for="creditorHouseNumber">
                  <b-form-input size="sm" id="creditorHouseNumberInput"
                                type="text"
                                name="Creditor House Number"
                                v-model="body.creditorInformation.creditor.houseNumber"
                                v-validate="'min:1|max:16'">
                  </b-form-input>
                  <b-input-group-append>
                    <b-button
                      variant="secondary"
                      v-b-tooltip.hover title="House number of the creditor
                       Maximum 16 characters permitted">?
                    </b-button>
                  </b-input-group-append>
                  <br/>
                  <i v-show="errors.has('Creditor House Number')" class="fa fa-warning"></i>
                  <span v-show="errors.has('Creditor House Number')" style="color: red" class="help is-danger">{{ errors.first('Creditor House Number') }}</span>
                </b-input-group>
              </b-form-group>
              <b-form-group>
                <b-input-group size="sm" prepend="Postal Code:" id="creditorPostalCodeLabel"
                               label-for="creditorPostalCode">
                  <b-form-input size="sm" id="creditorPostalCodeInput"
                                type="text"
                                name="Creditor Postcode"
                                v-model="body.creditorInformation.creditor.postalCode"
                                v-validate="'required|min:1|max:16'"
                                required>
                  </b-form-input>
                  <b-input-group-append>
                    <b-button
                      variant="secondary"
                      v-b-tooltip.hover title="Postal code of the creditor
                       Maximum 16 characters permitted
                       The postal code is always to be entered without a country code prefix.">?
                    </b-button>
                  </b-input-group-append>
                  <br/>
                  <i v-show="errors.has('Creditor Postcode')" class="fa fa-warning"></i>
                  <span v-show="errors.has('Creditor Postcode')" style="color: red" class="help is-danger">{{ errors.first('Creditor Postcode') }}</span>
                </b-input-group>
              </b-form-group>
              <b-form-group>
                <b-input-group size="sm" prepend="City:" id="creditorCityLabel"
                               label-for="creditorCity">
                  <b-form-input size="sm" id="creditorCityInput"
                                type="text"
                                v-model="body.creditorInformation.creditor.city"
                                name="Creditor City"
                                v-validate="'required|min:1|max:35'"
                                required>
                  </b-form-input>
                  <b-input-group-append>
                    <b-button
                      variant="secondary"
                      v-b-tooltip.hover title="City of the creditor
                       Maximum 35 characters permitted">?
                    </b-button>
                  </b-input-group-append>
                  <br/>
                  <i v-show="errors.has('Creditor City')" class="fa fa-warning"></i>
                  <span v-show="errors.has('Creditor City')" style="color: red" class="help is-danger">{{ errors.first('Creditor City') }}</span>
                </b-input-group>
              </b-form-group>
              <b-form-group>
                <b-input-group size="sm" prepend="Country:" id="creditorCountryLabel"
                               label-for="creditorCountry">
                  <b-form-input size="sm" id="creditorCountryInput"
                                type="text"
                                name="Creditor Country"
                                v-model="body.creditorInformation.creditor.country"
                                v-validate="'required|min:2|max:2'"
                                required>
                  </b-form-input>
                  <b-input-group-append>
                    <b-button
                      variant="secondary"
                      v-b-tooltip.hover title="Country of the creditor
                       Two-digit country code according to ISO 3166-1">?
                    </b-button>
                  </b-input-group-append>
                  <br/>
                  <i v-show="errors.has('Creditor Country')" class="fa fa-warning"></i>
                  <span v-show="errors.has('Creditor Country')" style="color: red" class="help is-danger">{{ errors.first('Creditor Country') }}</span>
                </b-input-group>
              </b-form-group>
              <b-form-group>
                <b-input-group size="sm" prepend="Account Number:" id="creditorAccountNumberLabel"
                               label-for="creditorAccountNumber">
                  <b-form-input size="sm" id="creditorAccountNumberInput"
                                type="text"
                                name="Creditor Account Number"
                                v-model="body.creditorInformation.iban"
                                v-validate="'required|min:21|max:21'"
                                required>
                  </b-form-input>
                  <b-input-group-append>
                    <b-button
                      variant="secondary"
                      v-b-tooltip.hover title="IBAN or QR-IBAN of the creditor
                       Should be 21 characters in length
                       Only IBANs with CH or LI country code permitted">?
                    </b-button>
                  </b-input-group-append>
                  <br/>
                  <i v-show="errors.has('Creditor Account Number')" class="fa fa-warning"></i>
                  <span v-show="errors.has('Creditor Account Number')" style="color: red" class="help is-danger">{{ errors.first('Creditor Account Number') }}</span>
                </b-input-group>
              </b-form-group>
            </div>
            <div class='p-4 segment card'>
              <h4 class="heading"><b>Payment</b></h4>
              <b-form-group>
                <b-input-group size="sm" prepend="Amount:" id="amountLabel"
                               label-for="amount">
                  <b-form-input size="sm" id="amountInput"
                                type="number"
                                name="Payment Amount"
                                v-model="body.paymentAmountInformation.amount"
                                step=0.01
                                v-validate="'between:0,999999999'">
                  </b-form-input>
                  <b-input-group-append>
                    <b-button
                      variant="secondary"
                      v-b-tooltip.hover title="The payment amount
                         The amount is to be entered without leading zeroes
                         It should include the decimal separator (.) and two decimal places">?
                    </b-button>
                  </b-input-group-append>
                  <br/>
                  <i v-show="errors.has('Payment Amount')" class="fa fa-warning"></i>
                  <span v-show="errors.has('Payment Amount')" style="color: red" class="help is-danger">{{ errors.first('Payment Amount') }}</span>
                </b-input-group>
              </b-form-group>
              <b-form-group>
                <b-input-group size="sm" prepend="Currency:" id="currencyLabel"
                               label-for="currency">
                  <b-form-select id="currencyInput"
                                 :options="currencies"
                                 name="Payment Currency"
                                 v-model="body.paymentAmountInformation.currency"
                                 v-validate="'required|min:3|max:3'"
                                 required>
                  </b-form-select>
                  <br/>
                  <i v-show="errors.has('Payment Currency')" class="fa fa-warning"></i>
                  <span v-show="errors.has('Payment Currency')" style="color: red" class="help is-danger">{{ errors.first('Payment Currency') }}</span>
                </b-input-group>
              </b-form-group>
              <b-form-group>
                <b-input-group size="sm" prepend="Date:" id="dateLabel"
                               label-for="date">
                  <b-form-input size="sm" id="dateInput"
                                type="date"
                                v-model="body.paymentAmountInformation.date">
                  </b-form-input>
                  <b-input-group-append>
                    <b-button
                      variant="secondary"
                      v-b-tooltip.hover
                      title="Due date on which, according to the biller, the payment should be paid, at the latest (according to the payment conditions)">
                      ?
                    </b-button>
                  </b-input-group-append>
                </b-input-group>
              </b-form-group>
            </div>
            <div class='p-4 segment card'>
              <h4 class="heading"><b>Reference</b></h4>
              <b-form-group>
                <b-input-group size="sm" prepend="Reference:" id="referenceLabel"
                               label-for="reference">
                  <b-form-input size="sm" id="referenceInput"
                                type="text"
                                name="Payment Reference"
                                v-model="body.paymentReference.reference"
                                v-validate="'min:0|max:25'">
                  </b-form-input>
                  <b-input-group-append>
                    <b-button
                      variant="secondary"
                      v-b-tooltip.hover title="Reference number
                       Should be either a QR reference or a Creditor Reference (ISO 11649)">?
                    </b-button>
                  </b-input-group-append>
                  <br/>
                  <i v-show="errors.has('Payment Reference')" class="fa fa-warning"></i>
                  <span v-show="errors.has('Payment Reference')" style="color: red" class="help is-danger">{{ errors.first('Payment Reference') }}</span>
                </b-input-group>
              </b-form-group>
              <b-form-group>
                <b-input-group size="sm" prepend="Reference Type:" id="referenceTypeLabel"
                               label-for="referenceType">
                  <b-form-select id="referenceType"
                                 :options="referenceTypes"
                                 name="Payment Reference Type"
                                 v-model="body.paymentReference.referenceType"
                                 v-validate="'required|min:3|max:4'"
                                 required>
                  </b-form-select>
                  <b-input-group-append>
                    <b-button
                      variant="secondary"
                      v-b-tooltip.hover title="Reference type (QR, ISO)
                     The following codes are permitted:
                     QRR – QR reference
                     SCOR – Creditor Reference (ISO 11649)
                     NON – without reference">?
                    </b-button>
                  </b-input-group-append>
                  <br/>
                  <i v-show="errors.has('Payment Reference Type')" class="fa fa-warning"></i>
                  <span v-show="errors.has('Payment Reference Type')" style="color: red" class="help is-danger">{{ errors.first('Payment Reference Type') }}</span>
                </b-input-group>
              </b-form-group>
              <b-form-group>
                <b-input-group size="sm" prepend="Additional Info:" id="additionalInformationLabel"
                               label-for="additionalInformation">
                  <b-form-textarea id="additionalInformation"
                                   name="Additional Information"
                                   v-model="body.paymentReference.unstructuredMessage"
                                   placeholder="Enter any additional information you want to provide"
                                   :rows="3"
                                   :max-rows="6"
                                   v-validate="'min:0|max:140'">
                  </b-form-textarea>
                  <b-input-group-append>
                    <b-button
                      variant="secondary"
                      v-b-tooltip.hover title="Additional information
                     Can be used to provide additional information to the biller">?
                    </b-button>
                  </b-input-group-append>
                  <br/>
                  <i v-show="errors.has('Additional Information')" class="fa fa-warning"></i>
                  <span v-show="errors.has('Additional Information')" style="color: red" class="help is-danger">{{ errors.first('Additional Information') }}</span>
                </b-input-group>
              </b-form-group>
            </div>
            <div class='p-4 segment card'>
              <h4 class="heading"><b>Ultimate Creditor</b></h4>
              <div style="margin-bottom: 10px;text-align-last:left;color: black">
                <b-form-checkbox class='checkbox' v-model="ultimateCreditor" v-on:change="ultimateCreditorUpdate()">Same as creditor
                </b-form-checkbox>
              </div>
              <div id="ultimateCreditorDiv" v-if="!ultimateCreditor">
                <b-form-group>
                  <b-input-group size="sm" prepend="Name:" id="ultimateCreditorNameLabel"
                                 label-for="ultimateCreditorName">
                    <b-form-input size="sm" id="ultimateCreditorNameInput"
                                  type="text"
                                  name="Ultimate Creditor Name"
                                  v-model="body.ultimateCreditor.name"
                                  v-validate="'min:1|max:70'">
                    </b-form-input>
                    <b-input-group-append>
                      <b-button
                        variant="secondary"
                        v-b-tooltip.hover title="Name or company of the ultimate creditor
                       Maximum 70 characters permitted
                       First name (optional, if available) and last name or company name.">?
                      </b-button>
                    </b-input-group-append>
                    <br/>
                    <i v-show="errors.has('Ultimate Creditor Name')" class="fa fa-warning"></i>
                    <span v-show="errors.has('Ultimate Creditor Name')" style="color: red" class="help is-danger">{{ errors.first('Ultimate Creditor Name') }}</span>
                  </b-input-group>
                </b-form-group>
                <b-form-group>
                  <b-input-group size="sm" prepend="Street:" id="ultimateCreditorStreetLabel"
                                 label-for="ultimateCreditorStreet">
                    <b-form-input size="sm" id="ultimateCreditorStreetInput"
                                  type="text"
                                  name="Ultimate Creditor Street"
                                  v-model="body.ultimateCreditor.streetName"
                                  v-validate="'min:1|max:70'">
                    </b-form-input>
                    <b-input-group-append>
                      <b-button
                        variant="secondary"
                        v-b-tooltip.hover title="Street/P.O. box of the ultimate creditor
                       Maximum 70 characters permitted; may not include any house or building number.">?
                      </b-button>
                    </b-input-group-append>
                    <br/>
                    <i v-show="errors.has('Ultimate Creditor Street')" class="fa fa-warning"></i>
                    <span v-show="errors.has('Ultimate Creditor Street')" style="color: red" class="help is-danger">{{ errors.first('Ultimate Creditor Street') }}</span>
                  </b-input-group>
                </b-form-group>
                <b-form-group>
                  <b-input-group size="sm" prepend="House Number:" id="ultimateCreditorHouseNumberLabel"
                                 label-for="ultimateCreditorHouseNumber">
                    <b-form-input size="sm" id="ultimateCreditorHouseNumberInput"
                                  type="text"
                                  name="Ultimate Creditor House Number"
                                  v-model="body.ultimateCreditor.houseNumber"
                                  v-validate="'min:1|max:16'">
                    </b-form-input>
                    <b-input-group-append>
                      <b-button
                        variant="secondary"
                        v-b-tooltip.hover title="House number of the ultimate creditor
                       Maximum 16 characters permitted">?
                      </b-button>
                    </b-input-group-append>
                    <br/>
                    <i v-show="errors.has('Ultimate Creditor House Number')" class="fa fa-warning"></i>
                    <span v-show="errors.has('Ultimate Creditor House Number')" style="color: red" class="help is-danger">{{ errors.first('Ultimate Creditor House Number') }}</span>
                  </b-input-group>
                </b-form-group>
                <b-form-group>
                  <b-input-group size="sm" prepend="Postal Code:" id="ultimateCreditorPostalCodeLabel"
                                 label-for="ultimateCreditorPostalCode">
                    <b-form-input size="sm" id="ultimateCreditorPostalCodeInput"
                                  type="text"
                                  name="Ultimate Creditor Postcode"
                                  v-model="body.ultimateCreditor.postalCode"
                                  v-validate="'min:1|max:16'">
                    </b-form-input>
                    <b-input-group-append>
                      <b-button
                        variant="secondary"
                        v-b-tooltip.hover title="Postal code of the ultimate creditor
                       Maximum 16 characters permitted; is always to be entered without a country code prefix.">?
                      </b-button>
                    </b-input-group-append>
                    <br/>
                    <i v-show="errors.has('Ultimate Creditor Postcode')" class="fa fa-warning"></i>
                    <span v-show="errors.has('Ultimate Creditor Postcode')" style="color: red" class="help is-danger">{{ errors.first('Ultimate Creditor Postcode') }}</span>
                  </b-input-group>
                </b-form-group>
                <b-form-group>
                  <b-input-group size="sm" prepend="City:" id="ultimateCreditorCityLabel"
                                 label-for="ultimateCreditorCity">
                    <b-form-input size="sm" id="ultimateCreditorCityInput"
                                  type="text"
                                  name="Ultimate Creditor City"
                                  v-model="body.ultimateCreditor.city"
                                  v-validate="'min:1|max:35'">
                    </b-form-input>
                    <b-input-group-append>
                      <b-button
                        variant="secondary"
                        v-b-tooltip.hover title="City of the ultimate creditor
                       Maximum 35 characters permitted">?
                      </b-button>
                    </b-input-group-append>
                    <br/>
                    <i v-show="errors.has('Ultimate Creditor City')" class="fa fa-warning"></i>
                    <span v-show="errors.has('Ultimate Creditor City')" style="color: red" class="help is-danger">{{ errors.first('Ultimate Creditor City') }}</span>
                  </b-input-group>
                </b-form-group>
                <b-form-group>
                  <b-input-group size="sm" prepend="Country:" id="ultimateCreditorCountryLabel"
                                 label-for="ultimateCreditorCountry">
                    <b-form-input size="sm" id="ultimateCreditorCountryInput"
                                  type="text"
                                  name="Ultimate Creditor Country"
                                  v-model="body.ultimateCreditor.country"
                                  v-validate="'min:2|max:2'">
                    </b-form-input>
                    <b-input-group-append>
                      <b-button
                        variant="secondary"
                        v-b-tooltip.hover title="Country of the ultimate creditor
                       Two-digit country code according to ISO 3166-1">?
                      </b-button>
                    </b-input-group-append>
                    <br/>
                    <i v-show="errors.has('Ultimate Creditor Country')" class="fa fa-warning"></i>
                    <span v-show="errors.has('Ultimate Creditor Country')" style="color: red" class="help is-danger">{{ errors.first('Ultimate Creditor Country') }}</span>
                  </b-input-group>
                </b-form-group>
              </div>
            </div>
            <div class='p-4 segment card'>
              <h4 class="heading"><b>Ultimate Debtor</b></h4>
              <b-form-group>
                <b-input-group size="sm" prepend="Name:" id="ultimateDebtorNameLabel"
                               label-for="ultimateDebtorName">
                  <b-form-input size="sm" id="ultimateDebtorNameInput"
                                type="text"
                                name="Ultimate Debtor Name"
                                v-model="body.ultimateDebtor.name"
                                v-validate="'min:1|max:70'">
                  </b-form-input>
                  <b-input-group-append>
                    <b-button
                      variant="secondary"
                      v-b-tooltip.hover title="Name or company of the ultimate debtor
                       Maximum 70 characters permitted; first name (optional, if available) and last name or company name.">
                      ?
                    </b-button>
                  </b-input-group-append>
                  <br/>
                  <i v-show="errors.has('Ultimate Debtor Name')" class="fa fa-warning"></i>
                  <span v-show="errors.has('Ultimate Debtor Name')" style="color: red" class="help is-danger">{{ errors.first('Ultimate Debtor Name') }}</span>
                </b-input-group>
              </b-form-group>
              <b-form-group>
                <b-input-group size="sm" prepend="Street:" id="ultimateDebtorStreetLabel"
                               label-for="ultimateDebtorStreet">
                  <b-form-input size="sm" id="ultimateDebtorStreetInput"
                                type="text"
                                name="Ultimate Debtor Street"
                                v-model="body.ultimateDebtor.streetName"
                                v-validate="'min:1|max:70'">
                  </b-form-input>
                  <b-input-group-append>
                    <b-button
                      variant="secondary"
                      v-b-tooltip.hover title="Street/P.O. Box of the ultimate debtor
                       Maximum 70 characters permitted; may not include any house or building number.">?
                    </b-button>
                  </b-input-group-append>
                  <br/>
                  <i v-show="errors.has('Ultimate Debtor Street')" class="fa fa-warning"></i>
                  <span v-show="errors.has('Ultimate Debtor Street')" style="color: red" class="help is-danger">{{ errors.first('Ultimate Debtor Street') }}</span>
                </b-input-group>
              </b-form-group>
              <b-form-group>
                <b-input-group size="sm" prepend="House Number:" id="ultimateDebtorHouseNumberLabel"
                               label-for="ultimateDebtorHouseNumber">
                  <b-form-input size="sm" id="ultimateDebtorHouseNumberInput"
                                type="text"
                                name="Ultimate Debtor House Number"
                                v-model="body.ultimateDebtor.houseNumber"
                                v-validate="'min:1|max:16'">
                  </b-form-input>
                  <b-input-group-append>
                    <b-button
                      variant="secondary"
                      v-b-tooltip.hover title="House number of the ultimate debtor
                       Maximum 16 characters permitted">?
                    </b-button>
                  </b-input-group-append>
                  <br/>
                  <i v-show="errors.has('Ultimate Debtor House Number')" class="fa fa-warning"></i>
                  <span v-show="errors.has('Ultimate Debtor House Number')" style="color: red" class="help is-danger">{{ errors.first('Ultimate Debtor House Number') }}</span>
                </b-input-group>
              </b-form-group>
              <b-form-group>
                <b-input-group size="sm" prepend="Postal Code:" id="ultimateDebtorPostalCodeLabel"
                               label-for="ultimateDebtorPostalCode">
                  <b-form-input size="sm" id="ultimateDebtorPostalCodeInput"
                                type="text"
                                name="Ultimate Debtor Postcode"
                                v-model="body.ultimateDebtor.postalCode"
                                v-validate="'min:1|max:16'">
                  </b-form-input>
                  <b-input-group-append>
                    <b-button
                      variant="secondary"
                      v-b-tooltip.hover title="Postal code of the ultimate debtor
                       Maximum 16 characters permitted; is always to be entered without a country code prefix.">?
                    </b-button>
                  </b-input-group-append>
                  <br/>
                  <i v-show="errors.has('Ultimate Debtor Postcode')" class="fa fa-warning"></i>
                  <span v-show="errors.has('Ultimate Debtor Postcode')" style="color: red" class="help is-danger">{{ errors.first('Ultimate Debtor Postcode') }}</span>
                </b-input-group>
              </b-form-group>
              <b-form-group>
                <b-input-group size="sm" prepend="City:" id="ultimateDebtorCityLabel"
                               label-for="ultimateDebtorCity">
                  <b-form-input size="sm" id="ultimateDebtorCityInput"
                                type="text"
                                name="Ultimate Debtor City"
                                v-model="body.ultimateDebtor.city"
                                v-validate="'min:1|max:35'">
                  </b-form-input>
                  <b-input-group-append>
                    <b-button
                      variant="secondary"
                      v-b-tooltip.hover title="City of the ultimate debtor
                       Maximum 35 characters permitted">?
                    </b-button>
                  </b-input-group-append>
                  <br/>
                  <i v-show="errors.has('Ultimate Debtor City')" class="fa fa-warning"></i>
                  <span v-show="errors.has('Ultimate Debtor City')" style="color: red" class="help is-danger">{{ errors.first('Ultimate Debtor City') }}</span>
                </b-input-group>
              </b-form-group>
              <b-form-group>
                <b-input-group size="sm" prepend="Country:" id="ultimateDebtorCountryLabel"
                               label-for="ultimateDebtorCountry">
                  <b-form-input size="sm" id="ultimateDebtorCountryInput"
                                type="text"
                                name="Ultimate Debtor Country"
                                v-model="body.ultimateDebtor.country"
                                v-validate="'min:2|max:2'">
                  </b-form-input>
                  <b-input-group-append>
                    <b-button
                      variant="secondary"
                      v-b-tooltip.hover title="Country of the ultimate debtor
                       Two-digit country code according to ISO 3166-1">?
                    </b-button>
                  </b-input-group-append>
                  <br/>
                  <i v-show="errors.has('Ultimate Debtor Country')" class="fa fa-warning"></i>
                  <span v-show="errors.has('Ultimate Debtor Country')" style="color: red" class="help is-danger">{{ errors.first('Ultimate Debtor Country') }}</span>
                </b-input-group>
              </b-form-group>
            </div>
            <div class="btn">
              <b-button type="reset" variant="secondary">Reset</b-button>
            </div>
          </b-form>
        </b-col>
        <b-col sm="12" md="12" lg="4" xl="4">
          <div class='p-4 segment card'>
            <h4 class="heading">QR Code Image</h4>
            <b-form @submit="getQRCodeImage" v-if="show" class="form-horizontal">
              <b-form-group>
                <b-input-group size="sm" prepend="Format:" id="qrCodeImageFormatLabel"
                               label-for="qrCodeImageFormat">
                  <b-form-select id="qrCodeImageFormat"
                                 :options="formats"
                                 v-model="qrCodeImage.format"
                                 required>
                  </b-form-select>
                </b-input-group>
              </b-form-group>
              <b-form-group>
                <b-input-group size="sm" prepend="Size:" id="imageSizeLabel"
                               label-for="imageSize"
                               append="px">
                  <b-form-input size="sm" id="imageSizeInput"
                                type="number"
                                v-model="qrCodeImage.size"
                                required>
                  </b-form-input>
                </b-input-group>
              </b-form-group>
              <div class="btn">
                <b-button type="submit" variant="primary">Download</b-button>
              </div>
            </b-form>
          </div>
          <div class='p-4 segment card'>
            <h4 class="heading">Payment Part</h4>
            <b-form @submit="getPaymentPart" v-if="show" class="form-horizontal">
              <b-form-group>
                <b-input-group size="sm" prepend="Format:" id="paymentPartFormatLabel"
                               label-for="paymentPartFormat">
                  <b-form-select id="paymentPartFormat"
                                 :options="formats"
                                 v-model="paymentPart.format"
                                 required>
                  </b-form-select>
                </b-input-group>
              </b-form-group>
              <b-form-group>
                <b-input-group size="sm" prepend="Language:" id="paymentPartLanguageLabel"
                               label-for="paymentPartLanguage">
                  <b-form-select id="paymentPartLanguage"
                                 :options="languages"
                                 v-model="paymentPart.language"
                                 required>
                  </b-form-select>
                </b-input-group>
              </b-form-group>
              <b-form-group>
                <b-input-group size="sm" prepend="Page Size:" id="paymentPartPageSizeLabel"
                               label-for="paymentPartPageSize">
                  <b-form-select id="paymentPartPageSize"
                                 :options="pageSizes"
                                 v-model="paymentPart.pageSize"
                                 required>
                  </b-form-select>
                </b-input-group>
              </b-form-group>
              <b-form-group>
                <b-input-group size="sm" prepend="Boundary Lines:" id="paymentPartBoundaryLinesLabel"
                               label-for="paymentPartBoundaryLines">
                  <b-form-select id="paymentPartBoundaryLines"
                                 :options="booleanValues"
                                 v-model="paymentPart.boundaryLines"
                                 required>
                  </b-form-select>
                </b-input-group>
              </b-form-group>
              <div class="btn">
                <b-button type="submit" variant="primary">Download</b-button>
              </div>
            </b-form>
          </div>
          <div class='p-4 segment card'>
            <h4 class="heading">Swiss Payment Code</h4>
            <b-form @submit="getSwissPaymentCode" v-if="show" class="form-horizontal">
              <div class="btn">
                <b-button type="submit" variant="primary">Download</b-button>
              </div>
            </b-form>
            <b-form-textarea id="swissPaymentCodeTextArea"
                             placeholder="Swiss Payment Code"
                             :rows="4"
                             v-model="swissPaymentCode.swissPaymentCodeText"
                             class='swissPaymentCode'
                             readonly
                             no-resize>
            </b-form-textarea>
          </div>
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  data () {
    return {
      body: {
        alternativeSchemes: {
          alternativeSchemeParameters: [
            ''
          ]
        },
        creditorInformation: {
          creditor: {
            city: 'Biel',
            country: 'CH',
            houseNumber: '1268/2/22',
            name: 'Robert Schneider AG',
            postalCode: '2501',
            streetName: 'Rue du Lac'
          },
          iban: 'CH4431999123000889012'
        },
        paymentAmountInformation: {
          amount: 199.95,
          currency: 'CHF',
          date: '2019-10-31'
        },
        paymentReference: {
          reference: 'RF18539007547034',
          referenceType: 'SCOR',
          unstructuredMessage: ''
        },
        ultimateCreditor: {
          city: 'Biel',
          country: 'CH',
          houseNumber: '1268/3/1',
          name: 'Robert Schneider Services Switzerland AG',
          postalCode: '2501',
          streetName: 'Rue du Lac'
        },
        ultimateDebtor: {
          city: 'Rorschach',
          country: 'CH',
          houseNumber: '28',
          name: 'Pia-Maria Rutschmann-Schnyder',
          postalCode: '9400',
          streetName: 'Grosse Marktgasse'
        }
      },
      response: {
        status: ''
      },
      currencies: [
        'EUR', 'CHF'
      ],
      referenceTypes: [
        'QRR', 'SCOR', 'NON'
      ],
      formats: [
        'image/png', 'application/pdf', 'image/tiff', 'image/gif'
      ],
      languages: [
        'de', 'fr', 'en', 'it'
      ],
      pageSizes: [
        'A4', 'A5', 'A6'
      ],
      booleanValues: [
        'true', 'false'
      ],
      ultimateCreditor: true,
      qrCodeImage: {
        format: 'image/png',
        size: 500
      },
      paymentPart: {
        format: 'image/png',
        language: 'de',
        pageSize: 'A6',
        boundaryLines: 'true'
      },
      swissPaymentCode: {
        swissPaymentCodeText: ''
      },
      show: true
    }
  },
  methods: {
    getQRCodeImage (evt) {
      this.$validator.validateAll().then((result) => {
        if (result) {
          evt.preventDefault()
          this.response.status = ''
          let url = 'http://qrinvoicerestdemo.eu-central-1.elasticbeanstalk.com/qr-invoice/swiss-qr-code?size=' + this.qrCodeImage.size
          let body = JSON.stringify(this.body, this.replacer)
          let config = {
            headers: {
              'Content-Type': 'application/json',
              'Accept': this.qrCodeImage.format
            },
            responseType: 'blob'
          }
          axios.post(url, body, config).then(response => {
            let a = document.createElement('a')
            a.href = window.URL.createObjectURL(response.data)
            a.download = 'QRCode' + '.' + this.qrCodeImage.format.substr(this.qrCodeImage.format.indexOf('/') + 1)
            a.style.display = 'none'
            document.body.appendChild(a)
            a.click()
            document.body.removeChild(a)
          }).catch(error => {
            let reader = new FileReader()
            reader.readAsText(error.response.data)
            reader.addEventListener('loadend', (e) => {
              this.response.status = this.getText(e)
            })
          })
        }
      })
    },
    getPaymentPart (evt) {
      this.$validator.validateAll().then((result) => {
        if (result) {
          evt.preventDefault()
          this.response.status = ''
          let url = 'http://qrinvoicerestdemo.eu-central-1.elasticbeanstalk.com/qr-invoice/payment-part?pageSize=' + this.paymentPart.pageSize + '&paymentPartBoundaryLines=' + this.paymentPart.boundaryLines
          let body = JSON.stringify(this.body, this.replacer)
          let config = {
            headers: {
              'Content-Type': 'application/json',
              'Accept': this.paymentPart.format,
              'Accept-Language': this.paymentPart.language
            },
            responseType: 'blob'
          }
          axios.post(url, body, config).then(response => {
            let a = document.createElement('a')
            a.href = window.URL.createObjectURL(response.data)
            a.download = 'PaymentPart' + '.' + this.paymentPart.format.substr(this.paymentPart.format.indexOf('/') + 1)
            a.style.display = 'none'
            document.body.appendChild(a)
            a.click()
            document.body.removeChild(a)
          }).catch(error => {
            let reader = new FileReader()
            reader.readAsText(error.response.data)
            reader.addEventListener('loadend', (e) => {
              this.response.status = this.getText(e)
            })
          })
        }
      })
    },
    getSwissPaymentCode (evt) {
      this.$validator.validateAll().then((result) => {
        if (result) {
          evt.preventDefault()
          this.response.status = ''
          let url = 'http://qrinvoicerestdemo.eu-central-1.elasticbeanstalk.com/qr-invoice/swiss-payments-code'
          let body = JSON.stringify(this.body, this.replacer)
          let config = {
            headers: {
              'Content-Type': 'application/json',
              'Accept': 'text/plain'
            }
          }
          axios.post(url, body, config).then(response => {
            this.swissPaymentCode.swissPaymentCodeText = response.data
          }).catch(error => {
            this.response.status = error.response.data
          })
        }
      })
    },
    onReset (evt) {
      evt.preventDefault()
      this.body.creditorInformation.creditor.country = ''
      this.body.creditorInformation.creditor.city = ''
      this.body.creditorInformation.creditor.postalCode = ''
      this.body.creditorInformation.creditor.houseNumber = ''
      this.body.creditorInformation.creditor.streetName = ''
      this.body.creditorInformation.creditor.name = ''
      this.body.creditorInformation.iban = ''
      this.body.ultimateDebtor.city = ''
      this.body.ultimateDebtor.country = ''
      this.body.ultimateDebtor.houseNumber = ''
      this.body.ultimateDebtor.name = ''
      this.body.ultimateDebtor.postalCode = ''
      this.body.ultimateDebtor.streetName = ''
      this.body.ultimateCreditor.city = ''
      this.body.ultimateCreditor.postalCode = ''
      this.body.ultimateCreditor.houseNumber = ''
      this.body.ultimateCreditor.name = ''
      this.body.ultimateCreditor.country = ''
      this.body.ultimateCreditor.streetName = ''
      this.body.paymentReference.unstructuredMessage = ''
      this.body.paymentReference.referenceType = ''
      this.body.paymentReference.reference = ''
      this.body.paymentAmountInformation.date = ''
      this.body.paymentAmountInformation.currency = ''
      this.body.paymentAmountInformation.amount = ''
      this.body.alternativeSchemes.alternativeSchemeParameters = ''
      this.show = false
      this.$nextTick(() => {
        this.show = true
      })
    },
    ultimateCreditorUpdate () {
      this.ultimateCreditor = !this.ultimateCreditor
    },
    getText (e) {
      let text
      if (e.target) {
        text = e.target.result
      } else if (e.srcElement) {
        text = e.srcElement.result
      }
      return text
    },
    replacer (key, value) {
      if (key === 'ultimateCreditor') {
        if (this.ultimateCreditor) {
          return undefined
        }
      }
      return value
    }
  }
}
</script>

<style scoped>
  .card {
    color: #AAABB8;
    background:#2b7a78;
    margin-bottom: 5%;
    box-shadow: 0 3px 6px rgba(0,0,0,0.16), 0 3px 6px rgba(0,0,0,0.23);
  }
  .heading {
    color: #feffff;
    font-weight: bold;
    text-align: center;
    margin-bottom: 15px;
  }
  .input-group-text{
    background:#17252a;
    color:#def2f1;
    border-color: #17252a;
  }
  .btn-secondary{
    background:#17252a !important;
    color:#def2f1;
    border-color: #17252a !important;
  }
  .btn-primary{
    background:#def2f1 !important;
    color:#17252a;
    border-color: #def2f1 !important;
  }
  .swissPaymentCode{
    background:#def2f1 !important;
    color:#17252a;
    border-color: #def2f1 !important;
  }
  .is-danger{
    width: inherit;
  }
  .form-input{
    width: max-content;
  }
  @media (min-width: 170px) {
    .input-group-prepend {
      width: 170px;
      background:#17252a;
      color:#def2f1;
      border-color: #17252a;
    }
  }
</style>
