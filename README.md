# seges-otrs-escalationindexbuild

Allows a SLA based on calendar days with an offset to the next working day if the start or final dates are non working days. That is, allows to use a SLA based on calendar days, in which the start and final dates could only be a working day.

## Requirements

* OTRS version 6.x or equivalent (like Znuny) with ITSM bundle.
* Znuny4OTRS-EscalationSuspend version 6.0.7 preinstalled.

## Installation

* Download the package in the release section.
* Install the package into OTRS.

# Use

* Set up the calendar days SLAs ids using the setting ```Core::CalendarDaysSLAs```.
* Set up the non working days of week using the setting ```Core::NonWorkingDaysOfWeek```.
* Set up the global vacation days.

# Roadmap

* Allows to set up a reference calendar, instead of use the global vacation days.
