# datacenter-registry

A prototype schema for FDSN data center registry exchange format and related information.

# Overview

The purpose of this repository is to support the development of a
schema, rules for use and examples of a JSON-based data format for
exchange of high-level data center information.  Each data center
entry may further specify data request routing rules.  The authors
intend to propose this format as a standard governed by FDSN WG II.

## Central registry

Services will be developed on www.fdsn.org to support a central
repository.  Data centers will be able to populate and update their
own entry through a web form or web service interface.  Furthermore, a
web service interface will be provided to allow clients to query the
repository for entries.

## Routing rules

A data center may specify one or more repositories with associated web
service interfaces.  Each repository entry may include routing rules
for time series data requests.  These rules are to be used to
determine the primary, secondary, etc. data center from which specific
data should be requested.

Each routing rule entry may specify a network, station, location,
channel, start time, end time and priority.  Each of these are
optional.  In the case of identifiers and time range, when missing
should be interpreted as "all", inclusively.  In the case of
priority, when missing should be interpreted as "unknown" and less
than any explicitly specified priority.

The central registry will include conflict detection to avoid the case
where the same data is directed to two data center repositories with
the same explicitly specified priority.

_NOTE_: data centers that do not include routing rules for data they
own or are otherwise delegated to serve must understand that users of
the central registry will use their own logic to determine from which
data center to request the data.  This only applies to cases where the
same data exist at multiple data centers.
