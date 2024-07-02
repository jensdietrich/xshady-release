# xshady-release

### Proof-of-vulnerability projects demonstrating the presence of vulnerabilities in projects cloning or shading vulnerable components.

The repository is organised by CVE. It contains projects that demonstrate the presence of a vulnerability in a component that is derived from the original component by means of shading or cloning, and does not declare a dependency to the original component.  The project titles are derived from the GAV coordinates (groupId+artifactId+version) of the vulnerable component, and the poms in each project declare a dependency to the vulnerable component. 

Since those components are deployed in Maven central and generally not listed in vulnerabilty databases like the [GHSA DB](https://github.com/github/advisory-database/) (at the time of commit), software composition analysis tool will generally miss those vulnerabilities. However, any client application using these packages that we report is potentially vulnerable in the same way as if was using the already indexed vulnerable original component.

To verify that a vulnerability is present, run `mvn test` for the respective project. Note that tests must _succeed_, not just _not fail_. Some tests declare preconditions on the OS or Java version (i.e. assumptions), and if those are not satisfied, tests will be marked as _skipped_. 

Each project folder also contains a subfolder `/scan-results` that contains the scan reports produced by several SCA tools. This is to demonstrate that those tools often miss vulnerabilities. As we disclose results, those gaps will be addressed and vulnerability databases will be updated, so those results are valid at the time of committing the respective reports.  

We have created a tool to find those components, and submitted a research paper describing the process. This will be made available here once the paper has been accepted. The project has been sponsored by Oracle Labs Australia, and is a collaboration between [Jens Dietrich](https://people.wgtn.ac.nz/jens.dietrich) (Victoria University of Wellington), [Alex Jordan](https://labs.oracle.com/pls/apex/f?p=labs:bio:0:2133) (Oracle Labs Austria) and [Shawn Rasheed](https://conf.researchr.org/profile/shawnrasheed) (UCOL). 

In a nutshell, the tool works as follows: 

1. The input is a vulnerable Maven artifact, i.e. a GAV identifying an artifact, and a test case to demonstrate a vulnerability (CVE) in this artifact. The test is embedded in a Maven project that has the artifact as a dependency, sample projects can be found in https://github.com/jensdietrich/xshady , we refer to those as __proof-of-vulnerability (POV)__ projects. 
2. From the artifact, a digital fingerprint is extracted that can be used to locate similar artifacts (deployed in Maven central).  
3. Once similar artifacts are located, cloning or shading is confirmed by running a custom type-2 clone analysis comparing the input artifact with the potential clone. This analysis ignores changes due to shading. 
4. To verify that a cloned/shaded artifact is exposed to the same vulnerability, a new POV is synthesized from the input POV for each clone – this generally involves changing the dependency (from the input artifact to the clone), and if shading was used, also changing package references (e.g., in *import* statements). 
5. This POVs is then tested (`mvn test`). If this succeeds, the clone is shown to be exposed to the CVE. 
6. The analysis is designed to be precise. 
