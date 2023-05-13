# xshady-release

### Proof-of-vulnerability projects demonstrating the presence of vulnerabilities in projects cloning or shading vulnerable components.

The repository is organised by CVE. It contains projects that demonstrate the precense of a vulnerability in a component that is derived from the original component by means of shading or cloning, and does not declare a dependency to the original component.  The project titles are derived from the vulnerable component, and the poms in each project declare a dependency to the vulnerable component. 

To verify that a vulnerability is present, run `mvn test` for the respective project. Note that tests must _succeed_, not just _not fail_. Some tests declare preconditions on the OS or Java version (i.e. assumptions), and if those are not satisfied, tests will be marked as _skipped_. 

Each project folder also contains a subfolder `/scan-results` that contains the scan reports produced by several SCA tools. This is to demonstrate that those tools often miss vulnerabilities. As we disclose results, those gaps will be addressed and vulnerability databases will be updated, so those results are valid at the time of committing the respective reports.  

We have created a tool to find those components, and submitted a research paper describing the process. This will be made available here once the paper has been accepted. 
