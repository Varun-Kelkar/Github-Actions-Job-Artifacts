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