# seges-otrs-escalationindexbuild
Allows a SLA based on calendar days with an offset to the next working day it the start or final dates are non working days

## Requirements

* OTRS version 6.x or equivalent with ITSM bundle.
* Znuny4OTRS-EscalationSuspend version 6.0.7 preinstalled.

## Installation

* Download the package in the release section.
* Install the package into OTRS.

# Use

* Set up the calendar days SLAs ids using the setting ```Core::CalendarDaysSLAs```.
* Set up the non working days of week using the setting ```Core::NonWorkingDaysOfWeek```.
