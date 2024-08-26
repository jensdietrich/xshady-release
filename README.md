# xshady-release

### Proof-of-vulnerability projects demonstrating the presence of vulnerabilities in projects cloning or shading vulnerable components.

The repository is organised by CVE. It contains projects synthesised by the [shade-detector](https://github.com/jensdietrich/shadedetector/) that demonstrate the presence of a vulnerability in a component that is derived from the original component by means of shading or cloning. Those projects do not declare a dependency to the original component.  The project titles are derived from the GAV coordinates (groupId+artifactId+version) of the vulnerable component. The poms in each project declare a dependency to the vulnerable component. 

Since those components are deployed in Maven Central and generally not listed in vulnerability databases like the [GHSA DB](https://github.com/github/advisory-database/) (at the time of commit), (metadata-based) software composition analysis tools will generally miss those vulnerabilities. However, any client application using these packages that we report is potentially vulnerable in the same way as if was using the already indexed vulnerable original component.

To verify that a vulnerability is present, run `mvn test` for the respective project. Some tests declare preconditions on the OS or Java version (i.e. assumptions), and if those are not satisfied, tests will be marked as _skipped_. Those projects are synthesised using a proof-of-vulnerability project for the original vulnerable project, for the semantics of the test (i.e. whether pass or fail indicates the vulnerability), check [the repository containing those templates](https://github.com/jensdietrich/xshady).

Each project folder also contains a subfolder `/scan-results` that contains the scan reports produced by several SCA tools. This is to demonstrate that those tools often miss vulnerabilities. As we disclose results, those gaps will be addressed and vulnerability databases will be updated, so those results are valid at the time of committing the respective reports.  

A paper describing this approach and the [shade-detector](https://github.com/jensdietrich/shadedetector/) toll will be presented at [SCORED'24](https://scored.dev/).  The project has been sponsored by [Oracle Labs Australia](https://labs.oracle.com/), and is a collaboration between [Jens Dietrich](https://people.wgtn.ac.nz/jens.dietrich) and [Tim White](https://github.com/wtwhite) (Victoria University of Wellington), [Alex Jordan](https://labs.oracle.com/pls/apex/f?p=labs:bio:0:2133) (Oracle Labs Austria) and [Shawn Rasheed](https://conf.researchr.org/profile/shawnrasheed) (UCOL). 

## Successful Disclosures 

|   CVE    | GHSA Update | Lib Name | 
| :---:       |    :----:        |   :----:        |  
| CVE-2022-38749  | https://github.com/github/advisory-database/pull/2273 | Commons Text |
| CVE-2015-6420   | https://github.com/github/advisory-database/pull/2326 | Apache Commons Collections |
| CVE-2018-10237  | https://github.com/github/advisory-database/pull/2444   | Guava |
| CVE-2021-44228  | https://github.com/github/advisory-database/pull/2445   | Log4J |
| CVE-2019-12402  | https://github.com/github/advisory-database/pull/2823   | Apache Commons Compress |
| CVE-2016-5394 | https://github.com/github/advisory-database/pull/2826   | Apache Sling |
| CVE-2016-6798 | https://github.com/github/advisory-database/pull/2827   | Apache Sling |
| CVE-2015-7501 | https://github.com/github/advisory-database/pull/2841   | Apache Commons Collections |
| CVE-2018-1324 | https://github.com/github/advisory-database/pull/2855   | Apache Commons Compress |
