



![](https://i.imgur.com/e39f5os.png)




![](https://i.imgur.com/dGwvaMc.png)



Create a New Project in SonarQube from `Dashboard > Create Project > Manually`

![](https://i.imgur.com/07lXlxe.png)

Name the folder according to the project from GitLab Repository and the Main Branch Name

![](https://i.imgur.com/05U6E99.png)

Select `With GitLab CI` option

![](https://i.imgur.com/rsBiHj0.png)


Select Options best describing the project 

`Maven` for Java Projects
`Gradle`
`.NET` for .NET Projects
`Others` for JS, TS, Go, Python, PHP ...

![](https://i.imgur.com/DAACjHG.png)

Go to GitLab to your Project Repository then `Repository > Files `  Add new file with ` + > New File `

![](https://i.imgur.com/ELFbUdh.png)

Name the new file as `sonar-project.properties`
and add these lines

	sonar.projectKey=<project-display-name>
	sonar.qualitygate.wait=true

and commit

![](https://i.imgur.com/72pJxze.png)

Before commit `.gitlab-ci.yml` file go to GitLab Project Repository

`Settings > CI/CD > Runners`  
Turn off `Shared runners`
and make sure a runner is enabled for this project if not
Click on `Enable for this project` which has status `active`


![](https://i.imgur.com/uoNieQc.png)


Similarly make a new file name it `.gitlab-ci.yml`

```
sonarqube-check:
  image: 
    name: sonarsource/sonar-scanner-cli:latest
    entrypoint: [""]
  variables:
    SONAR_USER_HOME: "${CI_PROJECT_DIR}/.sonar"  # Defines the location of the analysis task cache
    GIT_DEPTH: "0"  # Tells git to fetch all the branches of the project, required by the analysis task
  cache:
    key: "${CI_JOB_NAME}"
    paths:
      - .sonar/cache
  script: 
    - sonar-scanner
  allow_failure: true
  rules:
    - if: $CI_COMMIT_BRANCH == 'master'
```


Commit `.gitlab-ci.yml` and check the pipeline is in running state

![](https://i.imgur.com/E8iHSo6.png)

wait for the pipeline to complete `Job succeeded`

![](https://i.imgur.com/indxtr0.png)

Check on sonarqube dashboard for the project report

![](https://i.imgur.com/1rqSDVu.png)

![](https://i.imgur.com/5MLkXti.png)

`......`