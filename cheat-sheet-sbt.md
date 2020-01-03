# sbt-cheat-sheet
### Syntax
`% vs %%`

Difference between % and %% in library string contatentation:
When used before the artifact name, %%, sbt will add the project’s binary Scala version to the artifact name.

Keywords: Cross-building

Refrence: https://www.scala-sbt.org/1.x/docs/Library-Dependencies.html#Getting+the+right+Scala+version+with

### Configuration
`resolvers += Classpaths.typesafeReleases`

Adds the [Typesafe Ivy repository](http://repo.typesafe.com/typesafe/releases/) to the project (SBT doesn’t know about it by default)

Reference: https://alvinalexander.com/scala/how-configure-sbt-custom-repositories-resolvers