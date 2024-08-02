# open-rewrite-test-suite-example

[rewrite.yml](rewrite.yml) Contains two recipes

1. org.openrewrite.java.dependencies.ChangeDependency
```yaml
type: specs.openrewrite.org/v1beta/recipe
name: com.sihutch.ChangeDependencyExample
displayName: Change Gradle or Maven dependency example
recipeList:
  - org.openrewrite.java.dependencies.ChangeDependency:
      oldGroupId: javax.servlet
      oldArtifactId: javax.servlet-api
      newGroupId: jakarta.servlet
      newArtifactId: jakarta.servlet-api
      newVersion: 6.x
```

1. org.openrewrite.gradle.ChangeDependency

```yaml
type: specs.openrewrite.org/v1beta/recipe
name: com.sihutch.ChangeGradleDependencyExample
displayName: Change Gradle dependency example
recipeList:
    - org.openrewrite.gradle.ChangeDependency:
          oldGroupId: javax.servlet
          oldArtifactId: javax.servlet-api
          newGroupId: jakarta.servlet
          newArtifactId: jakarta.servlet-api
          newVersion: 6.x
```

[build.gradle](build.gradle) has the same dependency `javax.servlet:javax.servlet-api:3.1.0`
defined in the main `dependencies` section and also in the `dependencies` section of a jvm-test-suite. 

When either of the above recipes are run. Only the dependecy is the main `dependencies` section is changed as shown 
by the dryRun diff below

```diff
   1   │ diff --git a/build.gradle b/build.gradle
   2   │ index 93ab89e..a7440b9 100644
   3   │ --- a/build.gradle
   4   │ +++ b/build.gradle
   5   │ @@ -17,7 +17,7 @@ com.sihutch.ChangeGradleDependencyExample
   6   │  
   7   │  dependencies {
   8   │      rewrite("org.openrewrite.recipe:rewrite-java-dependencies:1.14.0")
   9   │ -    implementation"javax.servlet:javax.servlet-api:3.1.0"
  10   │ +    implementation"jakarta.servlet:jakarta.servlet-api:6.1.0"
  11   │  }
  12   │  
  13   │  testing {
  14   │ 
```