# Scenario 02 - Unsual POST probes

**Dataset:** Apache Access logs
**Tool:** Splunk

-------------------

##Scenario 
Still on Tier 1 SOC shift, with the same Apache logs datasets. After spike of 403's and 404's, that were previously analyzed, I'm asked to keep an eye out for anything beyond reconnaissance. Alert manager if scanning escalates to attempting to gain access.

-------------------

## Objective

  Analyze logs in order to review any attempts to gain access to webserver.

  -------------------

  ## Splunk Queriers
    index="weblog"
    index="weblog" method=POST

    -------------------

## Findings 
  - Multiple POST attempts for the same src_ip address 78.173.140.106
  - POST attempts from annotated src_ip address occur exactly on the hour.
  - Each attempt from the src_ip 78.173.140.106 is met with  ERROR code 404 (NOT FOUND) 

  -------------------

## Analysis
  - Hourly POST attempts by src_ip address 78.173.140.106 on NOT FOUND webpages suggest automation browsing on the webserver.

-------------------

## Assessment
  - Activity is classified as suspicious probing/ reconnaisance attempts on the webserver.
  - Although POST is occuring on webpage that is NOT FOUND, threat should be taken serious as this indicates automation is probing around webserver.
  - Likely Phase: Reconaissance

-------------------

## Recommendation
  - Block suspicious IP
  - Continue monitoring logs
  - Escalation not required yet.
