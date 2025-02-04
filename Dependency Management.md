# Dependency Management in Various Programming Languages

## 1. How Dependency Management Works in Different Languages

For **JavaScript/Node.js** projects, the `package.json` file lists all dependencies, and running `npm i` installs them. Other programming languages have their own **dependency management systems** and **file formats** to achieve the same goal. Here's how it works in other popular languages:

| Language       | Dependency File       | Package Manager       | Command to Install Dependencies       |
|----------------|-----------------------|-----------------------|---------------------------------------|
| **JavaScript** | `package.json`        | NPM/Yarn/PNPM         | `npm i` or `yarn install`             |
| **Python**     | `requirements.txt`    | pip                   | `pip install -r requirements.txt`     |
| **Python**     | `pyproject.toml`      | Poetry                | `poetry install`                      |
| **Ruby**       | `Gemfile`             | Bundler               | `bundle install`                      |
| **Java**       | `pom.xml`             | Maven                 | `mvn install`                         |
| **Java**       | `build.gradle`        | Gradle                | `gradle build`                        |
| **PHP**        | `composer.json`       | Composer              | `composer install`                    |
| **Go**         | `go.mod`              | Go Modules            | `go mod tidy`                         |
| **Rust**       | `Cargo.toml`          | Cargo                 | `cargo build`                         |
| **.NET**       | `.csproj`             | NuGet                 | `dotnet restore`                      |
| **Dart**       | `pubspec.yaml`        | Pub                   | `flutter pub get`                     |
| **Swift**      | `Package.swift`       | Swift Package Manager | `swift build`                         |
| **Elixir**     | `mix.exs`             | Mix                   | `mix deps.get`                        |
| **Clojure**    | `deps.edn`            | Clojure CLI           | `clojure -P`                          |
| **Perl**       | `cpanfile`            | cpanm                 | `cpanm --installdeps .`               |
| **R**          | `DESCRIPTION`         | install.packages()    | `install.packages("package_name")`    |

---

## 2. Example Dependency Files for Various Languages

### **JavaScript (`package.json`)**
```json
{
  "name": "my-node-project",
  "version": "1.0.0",
  "description": "A sample Node.js project",
  "main": "index.js",
  "scripts": {
    "start": "node index.js",
    "test": "jest"
  },
  "dependencies": {
    "express": "^4.18.2",
    "lodash": "^4.17.21"
  },
  "devDependencies": {
    "jest": "^29.5.0",
    "eslint": "^8.36.0"
  }
}
```
### **Python (`requirements.txt`)**
```
Flask==2.3.2
requests>=2.28.0
numpy==1.24.3
pytest==7.3.1
```
### **Python (`pyproject.toml` for Poetry)**
```
[tool.poetry]
name = "my-python-project"
version = "0.1.0"
description = "A sample Python project"
authors = ["Your Name <you@example.com>"]

[tool.poetry.dependencies]
python = "^3.8"
flask = "^2.3.2"
requests = "^2.28.0"

[tool.poetry.dev-dependencies]
pytest = "^7.3.1"
```
### **Ruby (`Gemfile`)**
```
source 'https://rubygems.org'

gem 'rails', '~> 7.0.4'
gem 'sqlite3', '~> 1.4'
gem 'puma', '~> 5.6'

group :development, :test do
  gem 'rspec-rails', '~> 6.0'
end
```

### **Java (`pom.xml` for Maven)**
```
<project>
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.example</groupId>
  <artifactId>my-java-project</artifactId>
  <version>1.0.0</version>

  <dependencies>
    <dependency>
      <groupId>org.junit.jupiter</groupId>
      <artifactId>junit-jupiter</artifactId>
      <version>5.9.2</version>
      <scope>test</scope>
    </dependency>
    <dependency>
      <groupId>com.google.guava</groupId>
      <artifactId>guava</artifactId>
      <version>31.1-jre</version>
    </dependency>
  </dependencies>
</project>
```

### **Java (`build.gradle` for Gradle)**
```
plugins {
    id 'java'
}

group 'com.example'
version '1.0.0'

repositories {
    mavenCentral()
}

dependencies {
    testImplementation 'org.junit.jupiter:junit-jupiter:5.9.2'
    implementation 'com.google.guava:guava:31.1-jre'
}

test {
    useJUnitPlatform()
}
```

### **PHP (`composer.json`)**
```
{
  "name": "my-php-project",
  "description": "A sample PHP project",
  "require": {
    "php": "^8.0",
    "laravel/framework": "^10.0"
  },
  "require-dev": {
    "phpunit/phpunit": "^10.0"
  }
}
```

### **Go (`go.mod`)**
```
module my-go-project

go 1.20

require (
    github.com/gorilla/mux v1.8.0
    github.com/stretchr/testify v1.8.4
)
```

### **Rust (`Cargo.toml`)**
```
[package]
name = "my-rust-project"
version = "0.1.0"
edition = "2021"

[dependencies]
serde = "1.0"
tokio = { version = "1.0", features = ["full"] }

[dev-dependencies]
assert_eq = "0.1.0"
```

### **.NET (`.csproj`)**
```
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>net7.0</TargetFramework>
  </PropertyGroup>

  <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="13.0.3" />
    <PackageReference Include="xunit" Version="2.4.2" />
  </ItemGroup>
</Project>
```

### **Dart/Flutter (`pubspec.yaml`)**
```
name: my_flutter_app
description: A sample Flutter project.
version: 1.0.0+1

dependencies:
  flutter:
    sdk: flutter
  http: ^0.13.3

dev_dependencies:
  flutter_test:
    sdk: flutter
```

### **Swift (`Package.swift`)**
```
// swift-tools-version:5.7
import PackageDescription

let package = Package(
    name: "MySwiftProject",
    dependencies: [
        .package(url: "https://github.com/vapor/vapor.git", from: "4.0.0")
    ],
    targets: [
        .target(
            name: "MySwiftProject",
            dependencies: [
                .product(name: "Vapor", package: "vapor")
            ]
        )
    ]
)
```

### **Elixir (`mix.exs`)**
```
defmodule MyApp.MixProject do
  use Mix.Project

  def project do
    [
      app: :my_app,
      version: "0.1.0",
      deps: deps()
    ]
  end

  defp deps do
    [
      {:plug, "~> 1.14"},
      {:ecto, "~> 3.9"}
    ]
  end
end
```

### **Clojure (`deps.edn`)**
```
{:deps
 {org.clojure/clojure {:mvn/version "1.11.1"}
  ring/ring-core {:mvn/version "1.9.5"}}}
```

### **Perl (`cpanfile`)**
```
requires 'Mojolicious', '== 9.31';
requires 'DBI', '>= 1.643';
on test => sub {
    requires 'Test::More', '== 0.98';
};
```

### **R (`DESCRIPTION`)**
```
Package: MyRPackage
Version: 0.1.0
Depends:
    R (>= 3.6.0)
Imports:
    dplyr,
    ggplot2
Suggests:
    testthat
```

