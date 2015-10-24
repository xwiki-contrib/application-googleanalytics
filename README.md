This extension allows to integrate Google Analytics Reports into XWiki, by providing a set of Macro to use in XWiki either on your Dashboard or on any page.

== How to install ==

To install you need to setup authentication with Google Analytics. To do this two methods are possible which are described below.

=== Authenticate using Client ID ===

This method will allow users to authenticate on their Google Account and access the reports for which they have rights on Google Analytics.
This method will not allow to show Google Analytics reports to non-authorized users.

Step 1/ Create a project and a client ID according to this Tutorial: https://developers.google.com/api-client-library/javascript/start/start-js#Setup
Step 2/ Make sure to not forget to set the "Authorized Javascript Origin" to the URL of your web server.
Step 3/ Make sure to add the Google Analytics API to the APIs available for your project (still in the developer console)
Step 4/ Finally add the client ID to your Google Analytics Embed API Configuration

=== Authenticate using a Service Account ===

This method will allow to authenticate on the server side and will not require users to log-in on their user account. 
This method allows to show Google Analytics reports to any users. Users that can edit in the wiki will allow to access most of the Google Analytics data authorized to the Service Account.

Setting-up server authentication is explain on the Google Analytics Embed API web site ( https://ga-dev-tools.appspot.com/embed-api/server-side-authorization/) and has a few steps:

Step 1/ Create a project and a service account according to this Tutorial: https://developers.google.com/identity/protocols/OAuth2ServiceAccount#creatinganaccount
Step 2/ Make sure to add the Google Analytics API to the APIs available for your project (still in the developer console)
Step 3/ Once created, download the "p12" file and save it to your server in /WEB-INF/GoogleAnalytics.p12 of your XWiki installation
 (usually in webapps/xwiki/WEB-INF/. If you don't have access to the server, ask your Hosting Administrator.)
Step 4/ Add the service account with read rights to your Google Analytics Account
Step 5/ Finally add the service account to your Google Analytics Embed API Configuration.

== Check the Demos ==

Verify your configration by accessing the Demo page in XWiki. This will also allow you to see the ID of your Google Analytics report which you can use in the macros in the next section.

== Use the Macros ==

The following macros are available:

=== gachart ===

This macro allows to add a chart of your Google Analytics data. This is a most common macro to use to make customized reports.

{{gachart /}}  

|= Parameter |= Default value |= Description
| clientid | The macro will use the client ID set in the Google Analytics Embed API Preferences of the local wiki, or if not present, of the main wiki. | Client ID used for Authentication
| serviceaccount | The macro will use the service account set in the Google Analytics Embed API Preferences of the local wiki, or if not present, of the main wiki. | Service Account used for Authentication if client ID is not set
| ids | None | ID of the Google Analytics tracked web site (ga:XXXXXXX). You can find out these values using the [[Demo]] page
| metrics | ga:sessions | One or more metric to display
| dimensions | ga:date | Field to use to break down the data
| sort | | Sorting field (this does not always make sense)
| start-date | 30DaysAgo | Start date of the period reported on
| end-date | yesterday | End date of the period reported on
| max-results | 6 | Maximum results to display (the remaining results are reported as "Other") 
| type | LINE | Type of report (LINE, COLUMN, BAR, TABLE, and GEO)
| width | 100% | Width of the report

=== googleanalytics ===

This macro allows to add you custom Google Analytics Embed API code to display any report. This macro requires developer skills.

{{googleanalytics}}  
.. js code ..
{{/googleanalytics}}  

|= Parameter |= Default value |= Description
| clientid | The macro will use the client ID set in the Google Analytics Embed API Preferences of the local wiki, or if not present, of the main wiki. | Client ID used for Authentication
| serviceaccount | The macro will use the service account set in the Google Analytics Embed API Preferences of the local wiki, or if not present, of the main wiki. | Service Account used for Authentication if client ID is not set
| content field | | The content field of the macro should be Javascript code written to the Embed API
