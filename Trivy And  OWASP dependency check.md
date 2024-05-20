## Going to scan dependences which are using in our project (java====pom.xml,,,,,,nodejs====package.json,,,,,,,,,,python=====requirements.txt).
1) Trivy has access to NVD(national vulnerabuls database) which contains all vulnerability  from 2002 to 2024...
2) trivy download that database and compare that database with our dependences..
3) trivy is more better than OWASP dependency check because OWASP has only access to NVD,,but trivy can access to other databases like redhat linux,,other linux flavours 


---INSTALLATION STEPS---

sudo apt-get install wget apt-transport-https gnupg lsb-release

wget -qO - https://aquasecurity.github.io/trivy-repo/deb/public.key | gpg --dearmor | sudo tee /usr/share/keyrings/trivy.gpg > /dev/null

echo "deb [signed-by=/usr/share/keyrings/trivy.gpg] https://aquasecurity.github.io/trivy-repo/deb $(lsb_release -sc) main" | sudo tee -a /etc/apt/sources.list.d/trivy.list

sudo apt-get update

sudo apt-get install trivy


---COMMANDS---

trivy image imagename

trivy fs --security-checks vuln,config   Folder_name_OR_Path

trivy image --severity HIGH,CRITICAL image_name

trivy image -f json -o results.json image_name

trivy repo repo-url

trivy k8s --report summary cluster

*******************************************************************************************************************************************************************

# Dependency-Check

Dependency-Check is a Software Composition Analysis (SCA) tool that attempts to detect publicly disclosed vulnerabilities contained within a project's dependencies. It does this by determining if there is a Common Platform Enumeration (CPE) identifier for a given dependency. If found, it will generate a report linking to the associated CVE entries.

Documentation and links to production binary releases can be found on the [github pages](http://jeremylong.github.io/DependencyCheck/). Additionally, more information about the architecture and ways to extend dependency-check can be found on the [wiki].

## Requirements

### Java Version

Minimum Java Version: Java 8 update 251

While dependency-check 9.0.0 and higher will still run on Java 8 - the update version
must be higher then 251.

### Internet Access

OWASP dependency-check requires access to several externally hosted resources.
For more information see [Internet Access Required](https://jeremylong.github.io/DependencyCheck/data/index.html).

### Build Tools

In order to analyze some technology stacks dependency-check may require other
development tools to be installed. Some of the analysis listed below may be
experimental and require the experimental analyzers to be enabled.

1. To analyze .NET Assemblies the dotnet 6 run time or SDK must be installed.
   - Assemblies targeting other run times can be analyzed - but 6 is required to run the analysis.
2. If analyzing GoLang projects `go` must be installed.
3. The analysis of `Elixir` projects requires `mix_audit`.
4. The analysis of `npm`, `pnpm`, and `yarn` projects requires `npm`, `pnpm`, or `yarn` to be installed.
   - The analysis performed utilize the respective `audit` feature of each.
5. The analysis of Ruby is a wrapper around `bundle-audit`, which must be installed.

## Current Releases

### Jenkins Plugin

For instructions on the use of the Jenkins plugin please see the [OWASP Dependency-Check Plugin page](https://wiki.jenkins-ci.org/display/JENKINS/OWASP+Dependency-Check+Plugin).


### Command Line

More detailed instructions can be found on the
[dependency-check github pages](http://jeremylong.github.io/DependencyCheck/dependency-check-cli/).
The latest CLI can be downloaded from github in the [releases section](https://github.com/jeremylong/DependencyCheck/releases).

Downloading the latest release:
```
$ VERSION=$(curl -s https://jeremylong.github.io/DependencyCheck/current.txt)
$ curl -Ls "https://github.com/jeremylong/DependencyCheck/releases/download/v$VERSION/dependency-check-$VERSION-release.zip" --output dependency-check.zip
```

On *nix
```
$ ./bin/dependency-check.sh -h
$ ./bin/dependency-check.sh --out . --scan [path to jar files to be scanned]
```

### Maven Plugin

More detailed instructions can be found on the [dependency-check-maven github pages](http://jeremylong.github.io/DependencyCheck/dependency-check-maven).
By default, the plugin is tied to the `verify` phase (i.e. `mvn verify`). Alternatively,
one can directly invoke the plugin via `mvn org.owasp:dependency-check-maven:check`.

The dependency-check plugin can be configured using the following:

```xml
<project>
    <build>
        <plugins>
            ...
            <plugin>
              <groupId>org.owasp</groupId>
              <artifactId>dependency-check-maven</artifactId>
              <executions>
                  <execution>
                      <goals>
                          <goal>check</goal>
                      </goals>
                  </execution>
              </executions>
            </plugin>
            ...
        </plugins>
        ...
    </build>
    ...
</project>
```
### Link 
https://github.com/jeremylong/DependencyCheck/blob/main/README.md?plain=1



