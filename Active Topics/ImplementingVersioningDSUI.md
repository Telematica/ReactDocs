Implementing versioning in the ds-ui-react repo
=


We need to implement proper versioning in our ds-ui-react repo. Doing this will allow us to have control over what version we are on and how that reflects the changes within the new version.




[If you don't understand how semantic versioning is supposed to work, please go to this link and read about it.](https://docs.npmjs.com/getting-started/semantic-versioning)


Basic description is that X.Y.Z is MAJOR.MINOR.PATCH. You update patch if it is a fix, you update minor if the changes are new and backwards compatible, and you update major if they are not.


This is how it works currently.


1. You make your changes and make a pr to master.
2. When a pr is merged to master, the pipeline build increments the patch version of the package.json and commits it to master.

This is bad for a couple of reasons.

1. It gives us no control.
2. If changes are not backwards compatible we have no knowledge of it because we are not using versions properly.
3. Pipeline build is changing source files?? What??


This is how it should work.

1. You make your changes and make a pr to master.
2. If your branch is a fix, but adds no new functionality, you increment the patch version of the package.json. This would likely not be done often.
3. If your branch is not a fix, we need to determine if your changes are backwards compatible or not.
   * If your branch is backwards compatible, you increment the minor version of the package.json.
     * Reset the patch number to 0.
   * If your branch is not backwards compatible, you incement the major version of the package.json.
     * Reset the minor and patch versions to 0.
4. Write patch notes! We need a confluence section that is a living document of patch notes. We should require this to be done and linked on the pr before any changes are merged.
5. Merge your branch into master.




So the big change here is that we would pull out the version changing in pipelines and do it manually. This seems more complicated but it gives us so much control over the process and allows us to version things properly. The biggest issue here is merge conflicts. I don't quite see a clear solution to this, so this is a point that needs discussion.