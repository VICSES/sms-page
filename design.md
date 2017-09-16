# Requirements

## Core

* Send an SMS to a phone number. SMS is paged out.

## Desirable

* Restrict SMS functionality to known numbers.
* Restrict web page functionality to Twilio source.
* Retain log of all messages sent

## Nice-to-have

* Support multiple units
* Ability to update phone numbers
* Provide pageing log via webpage


# Design

## Components

* Twilio for incoming and outgoing SMS control
* AWS Lambda instance running Flask to process incoming SMS
* AWS Lambda instance running Flask to perform admin tasks
* DynamoDB tables for data storage

## Twilio

* Twilio owns number
* Twilio contacts web page on incoming SMS
* Reply SMS sent on error

## Lambda to process incoming SMS

* Test for twilio signature to ensure origin
* Lookup phonenumber to ensure permission to use
* Lookup unit to get pager number
* Send admin page with sms body to unit number
* On success, no response
* On error and twilio signature, send SMS reply with details

## Lambda to process admin

* Log in using Microsoft login
* Lookup contact in contacts table
* Use permissions to determine access level
* Only show content and links if permission is granted
* Try and keep it all in one page if possible
* Basic CRUD REST APIs might be the way to go


## DynamoDB tables

* contacts
  * phone number (hash)
  * unit
  * name
  * member id (GSI hash)
  * permissions (json dict)
    * page log read
	* contacts read
	* contacts write
	* unit admin
	* site admin

* page log
  * unit (hash)
  * timestamp (range)
  * phone number
  * body

* unit
  * name (hash)
  * page id


