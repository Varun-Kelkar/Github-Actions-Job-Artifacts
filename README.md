## Job Artifacts

In layman's terms, any kind of output produced by a job can be called artifact.
In Github Actions, the job artifact can be uploaded downloaded(manually & automatically) as well used by other jobs. 


Action used - actions/upload-artifact


### Uploading Artifacts
```bash
steps: 
    -   name: <Step Name>
        uses: actions/upload-artifact@v3 <Action Name>
        with:
            name: dist-files <Name of the Artifact>
            path: dist <Files that we want to upload>
```

### Downloading Artifacts
```bash
steps:
    - name: <Step Name>
      uses: actions/download-artifact@v3 <Action Name>
        with:
          name: dist-files <Name of the Artifact should be same as the one used to upload>
```

### Dependency Caching

Since every job runs in its own execution environment, there are certain steps we need to repeat.

For eg - 

```bash
 - name: Install dependencies
   run: npm ci
```

Since dependencies don't change that frequently, we can cache them.

```bash
      - name: Caching Dependencies 
        uses: actions/cache@v3
        with:
          path: ~/.npm <Cache Path> <For npm install the path is always ~/.npm>
          key: deps-node-modules-${{ hashFiles('**/package-lock.json') }} <Unique Identifier for Cache>
      - name: Install dependencies
        run: npm ci
```

The Caching step should be before the step where we actually install dependencies.

The "key" is a unique identifier for a cache.

It should always be a combination of static + dynamic values

#### hashFiles()

Its a function provided by Github Actions which generates a unique hash based on a input value
