# External OSS Builds

Jenkinsfiles that build OSS projects (Spring Boot, Spring Framework, Airlift,
Dropwizard, Micrometer, CometD, …) against a chosen Jetty version to verify
backward compatibility. Builds run on Jenkins (https://jenkins.webtide.net,
jobs under `external_oss/`), not locally.

## Deploying changes
Jenkins builds these files from `jetty-project/external-oss-builds@master`.
Local edits have NO effect until committed **and pushed to master**; then
trigger a rebuild. Inspect builds via the `jetty-jenkins` MCP server.

## Shared init script
`init.gradle.spring-framework` is stashed and unstashed into the workspace
root, and is shared by the spring-boot, spring-framework and micrometer jobs.
A change here affects all of them.

## Gotchas
- **Jetty version override:** use `resolutionStrategy.eachDependency { useVersion }`,
  NOT `dependencySubstitution { useTarget }`. `useTarget` replaces the selector
  and drops the Jetty BOM constraint, breaking Spring Boot's
  `checkRuntimeClasspathForUnconstrainedDirectDependencies`.
- **Internal Nexus mirror is http-only** (`http://nexus-service...`). This trips
  Spring Framework's `checkstyleNohttp`. That task's source is convention-mapped,
  so `.exclude` is ignored — disable the task instead (`enabled = false`).
