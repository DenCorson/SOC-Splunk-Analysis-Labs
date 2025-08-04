# Scenario 01 - Unsual Traffic and Spike

**Dataset:** Apache Access Logs
**Tool:** Splunk

-------------------

## Scenario 
I am a Tier 1 SOC analyst on shift. A web server in my company's environment has reported  slowness and a spike in 403/404 errors. I will check out the Apache logs to figure out whats going on.

-------------------

## Objective

  Investigate reported spike in 403/404 errors on a company webserver and determine whether activity is benign or malicous.

  -------------------

## Splunk Queries
  index="weblog" status=404 OR status=403 | stats count(status) AS count by status | sort -count
  
  index=weblog status=404 OR status=403 | stats count(method) AS count by method

  -------------------

## Findings
 - Large spike in 403/404 errors withhin a short timeframe.
 - More than 200 GET requests during a one-hour period.
 - Requests targeted uncommon files:
    - config.xml
    - logon.php?action=register
    - /joomla/administrator/
- Traffic used mixed user agents (Mozzila, Googlebot, Chef Client)

  -------------------

## Analysis
 - The volume & short timeframe suggests automation rather than human browsing. 
 - Requests to rare endpoints and login pages indicate probing/reconnaissance.
 - User-agent rotation is consistent with automated scanning tools.

-------------------

Assessment
 - Activity classified as suspicious reconnaissance.
 - No evidence of compromise at the stage.
 - Likely phase: Reconnaissance

-------------------

Recommendation
 - Block suspicious IPs.
 - Continue monitoring for escaltion
