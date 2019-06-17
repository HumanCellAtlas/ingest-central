# Ingest SOP's

## Ingest release process 
[Release process using tagged builds](https://github.com/rdgoite/hca-developer-tools#release-process-using-tagged-builds)

```
dev
---o--->
   5ddba2b

integration
---o---o--->
       5ddba2b

staging
---o---o---o--->
           5ddba2b, v1.0.rc

production
---o---o---o---o
               5ddba2b, v1.0.rc, v1.0
```

## Releasing to dev and integration
    1. Create feature branch based from master
    2. Create a PR. Indicate the ZenHub ticket.
    3. Merge to master
        a. Requires tests passing (unit, ingest integration tests) - deploy image of commit in dev
        b. Requires 1-2 reviewers approval
        c. Code coverage should not go down
    4. After merge. Tag that commit. You could use the `git release` tool  [here](https://github.com/rdgoite/hca-developer-tools/blob/master/gitconfig). Quay.IO will automatically build images for tagged commits.
    5. Redeploy image to dev and integration. See ingest-kube-deployments repo for instructions on [How to Deploy](https://github.com/HumanCellAtlas/ingest-kube-deployment#deploy-and-upgrade-ingest-applications)
    6. Make sure all tests are passing (unit, ingest integration tests, DCP wide integration tests).
    7. If tests are failing because of the changes, redeploy back the previous image in integration and fix the tests in dev. 
    8. Update integration changelog. This will help the release engineer to know which components and what changes are needed to be release in staging. If we have some extra instructions for deployment, we could note it in the changelog. (not really sure where to put this)


## Releasing to staging and production
All changes in integration will soon be promoted to staging -> production in line with the DCP release 
[SOP: Releasing New Versions of DCP software](https://allspark.dev.data.humancellatlas.org/dcp-ops/docs/wikis/SOP:%20Releasing%20new%20Versions%20of%20DCP%20Software)


## Releasing hotfixes
    1. Inform the team of the hotfix. Team will decide if hotfix is needed and safe.
    2. Branch from the commit hash currenlty deployed in staging.
    3. Tag the commit. Deploy to staging. All tests must passed (DCP tests in staging, ingest tests, unit tests)
    5. Make a hotfix release note in DCP Release Notes directory
    6. Inform DCP Release manager(currently Rhian) 
    7. Deploy to prod. Make sure all tests
    

## Links
* [DCP Integration Tests](https://allspark.dev.data.humancellatlas.org/HumanCellAtlas/dcp?nav_source=navbar)
* [Ingest Integration Tests](https://allspark.dev.data.humancellatlas.org/HumanCellAtlas/ingest-integration-tests?nav_source=navbar)
* [DCP Release Notes](https://drive.google.com/drive/u/0/folders/16BU1y3n1SD7D5Q1NNk0YUgs4NG7ArWiu)
