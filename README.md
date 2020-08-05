# CiviCRM Ubercart integration

This module is an optional part of the [Ubercart
module](http://drupal.org/project/ubercart) and exists to integrate Ubercart
functions with CiviCRM.

## What it does

When a customer buys something from the Ubercart store, the name and address
information they provide is added to CiviCRM. If the customer has a simple
contact record generated by syncing CiviCRM from the Drupal user table, that
record is updated with the new information. If no contact record exists, one is
created.

Then the new or updated contact is added to the 'Purchasers' group or group
selected in the admin screen. A contribution record is added to the contact's
history and the 'Purchases' tab on the contact's dashboard entry is populated
with a link to the contact's order history in Ubercart.

## To install this module

- Copy the `uc_civicrm` directory into your Drupal modules directory
  (typically `{webroot}/sites/all/modules/`)

- Then visit the `admin/build/modules` page and enable "Ubercart/CiviCRM
  Integration" module in the "Ubercart - extra" section.

- Add location types `Ubercart_Billing` and `Ubercart_Shipping` in CiviCRM to
  store shipping and billing address

## Developers' notes

Note from @eileenmcnaughton in 2014: @todo - use `_uc_civicrm_get_locations()`
to specify location type rather than hard-coded names & build a form to set the
types

Notes from @artfulrobot Jan 2019:

- I have updated this to work with CiviCRM v5.4 as many things had become broken
  in the time since the last release. I cannot guarantee that I have tested
  every part of it, but contacts are being added/updated and purchases are being
  logged in CiviCRM as contributions again now. I incorporated some of the
  patches submitted in the github issue queue, but most of those are since
  absorbed in a bigger refactor.

- The logic of finding an existing contact for an order is not ideal and not
  well documented. It ought to use CiviCRM's dedupe rules to help find a
  contact, and ideally it could check for and use Systopia's Xtended Contact
  Matcher plugin, if it is available. There are questions over who the contact
  is if the billing and delivery and logged-in-user details are different.

