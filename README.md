Design Specifications for MSF CogniCity
=======================================

## Required Interfaces
- login page
- landing / overview page
  - showing locations of current events & their metadata
  - highlighting important items from external feeds
- map page:
  - view reports
  - get a share the map link
  - get an add report link
  - see contacts in the region
  - see previous reports from the region
- map page (with editing capabilities):
  - create an event with metadata
  - close and archive currently open events
  - add a report directly
- report card:
  - add a report, tied to specific event

## Core Functionality
- create and store events with persistent links
- create and store reports tied to an event
- access and filter database of existing contacts and previous activities
- support secure authorization

## Architecture
- PostgreSQL w/ PostGIS
- NodeJS application to expose APIs
  + Front-end client to render maps and pages as SPA or NodeJS express App
- Document store for other reports and contacts?

### Schema
- Tables
  - Events (ID, status, type, geometry, metadata)
  - Reports (ID, EVENT_ID, status, timestamp with time zone, geometry, report_content)
  - Contacts(ID, location, contact_details)

### API
GET /events - get a list of all events in system, returned as event objects
POST /events - makes a new event, and returns an event object for the new event

GET /events/:id - gets an event object for the specified event
POST /events/:id - updates an event object for the event, returns an event object for the specified event

GET /events/:id/reports - get a list of all reports for an event, returned as report objects
GET /events/:id/reports/:id - get a specified report, returned as a report object
POST /events/:id/reports/:hash - make a new report, authenticated against an existing link hash, returns report object
