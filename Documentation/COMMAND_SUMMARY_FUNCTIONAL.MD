# Summary of StoreBroker Commands (Functional Groupings)

The following is an listing of StoreBroker commands with brief descriptions, grouped by
areas of functionality. All aliases are documented.

Note: This is only summary information. For fuller documentation of StoreBroker commands,
use the PowerShell Get-Help command.

Some details on required inputs and return values are mentioned to provide more clarity
regarding the basic functionality of certain command. Note: if either required inputs or
a return value are mentioned, then all required inputs and any return value will be
covered.

Many StoreBroker commands directly correspond to Microsoft Store submission REST APIs.
For some commands, links are provided to documentation for the corresponding REST API or
related resources/objects.

-----
## Working with Applications, Flights and In-App Products

### Get-Application

<dl><dd>
</dd></dl>

### Get-ApplicationFlight

<dl><dd>
</dd></dl>

### Get-ApplicationFlights

<dl><dd>
</dd></dl>

### Get-ApplicationInAppProducts

<dl><dd>
</dd></dl>

### Get-Applications

<dl><dd>
</dd></dl>

### Get-FlightGroups

<dl><dd>
</dd></dl>

### Get-InAppProduct

<dl><dd>
</dd></dl>

### Get-InAppProducts

<dl><dd>
</dd></dl>

### New-ApplicationFlight

<dl><dd>
</dd></dl>

### New-InAppProduct

<dl><dd>
</dd></dl>

### Remove-ApplicationFlight

<dl><dd>
</dd></dl>

### Remove-InAppProduct

-----
## Working with Application Submissions

### Complete-ApplicationSubmission

<dl><dd>

**Alias:** Commit-ApplicationSubmission

Commits the specified application submission so that it can start the approval process.

Once committed, it is necessary to wait for the submission to either complete or fail the approval process before a new application submission can be created/submitted.

Note: This completes the submission API transaction, but not necessarily the publication
of the submission. The decision whether to publish after successful certification depends
on the TargetPublishMode setting when the submission was created.

Wraps the [commit](https://docs.microsoft.com/en-us/windows/uwp/monetize/commit-an-app-submission) Microsoft Store Submission API.

**Required inputs:**
- AppId
- SubmissionId

**Returns:** A status. (See [JSON response body](https://docs.microsoft.com/en-us/windows/uwp/monetize/commit-an-app-submission#response).)

</dd></dl>

### Complete-ApplicationSubmissionPackageRollout

<dl><dd>
</dd></dl>

### Get-ApplicationSubmission

<dl><dd>

Gets the details of a specific application submission.

Wraps the [submissions](https://docs.microsoft.com/en-us/windows/uwp/monetize/get-an-app-submission) Microsoft Store Submission API.

**Required input:**
- AppId
- SubmissionId

**Returns:** A [submission resource](https://docs.microsoft.com/en-us/windows/uwp/monetize/manage-app-submissions#app-submission-object) object \<PSCustomObject>

</dd></dl>

### Get-ApplicationSubmissionPackageRollout

<dl><dd>
</dd></dl>

### Get-ApplicationSubmissionStatus

<dl><dd>

Gets just the status of a specific application submission.

Wraps the [status](https://docs.microsoft.com/en-us/windows/uwp/monetize/get-status-for-an-app-submission) Microsoft Store Submission API.

**Required inputs:**
* AppId
* SubmissionId

**Returns:** A [status response](https://docs.microsoft.com/en-us/windows/uwp/monetize/get-status-for-an-app-submission#response) object \<PSCustomObject>

</dd></dl>

### Get-SubmissionPackage

<dl><dd>
</dd></dl>

### Join-SubmissionPackage

<dl><dd>
</dd></dl>

### New-ApplicationSubmission

<dl><dd>

Creates a submission for an existing application on the developer account.

This app must already have at least one *published* submission completed via the
Dev Portal in order for this function to work. The submission that is returned is
a clone of the currently-published submission.

You cannot submit a new application submission if there is an existing pending
application submission for $AppId already.  You can use -Force to work around this.

Wraps the [Create an App Submission](https://docs.microsoft.com/en-us/windows/uwp/monetize/create-an-app-submission) Microsoft Store Submission API.

**Required inputs:**
- AppId

**Returns:** A [submission](https://docs.microsoft.com/en-us/windows/uwp/monetize/manage-app-submissions#app-submission-object) object \<PSCustomObject>

</dd></dl>

### New-StoreBrokerConfigFile

<dl><dd>

**Alias:** New-PackageToolConfigFile

Creates a new configuration file as a template for an app submission.

The full path to the new file can be provided by the -Path parameter.

**Required inputs:** Path (for generated SBConfig.json file)

</dd></dl>

### New-SubmissionPackage

<dl><dd>

Top-level function for creating an application submission's JSON body
and .zip package for upload.

Creates the JSON body for a submission request.  Localized listing metadata
is taken from the path specified in the config file.
    
The .appxbundle, .appxupload, and .appx files are given via the -AppxPath parameter.
    
In the process of creating the JSON, the packaging tool also copies any specified
images and .appx files to a .zip file.
    
The .json and .zip files generated by this tool are given the common name specified by the -OutName parameter.

If AppId is specified, values in the JSON file will be set based on the most recent submission for that app.

**Required / optional inputs:**
* ConfigPath (existing SBConfig.json file)
* [AppId]

</dd></dl>

### Remove-ApplicationSubmission

<dl><dd>

Deletes the specified application submission from a developer account.

An app can only have a single "pending" submission at any given time,
and submissions cannot be modified via the REST API once started.
Therefore, before a new application submission can be submitted,
this method must be called to remove any existing pending submission.

Wraps the [Delete an App Submission](https://docs.microsoft.com/en-us/windows/uwp/monetize/delete-an-app-submission) Microsoft Store Submission API.

**Required inputs:**
- AppId
- SubmissionId

</dd></dl>

### Set-ApplicationSubmission

<dl><dd>

**Alias:** Replace-ApplicationSubmission

Replaces the content of an existing application submission with the supplied submission content.

This should be called after having cloned an application submission via New-ApplicationSubmission.

The ID of the submission being updated/replaced will be inferred by the
submissionId defined in UpdatedSubmission.

Wraps the [Update an App Submission](https://docs.microsoft.com/en-us/windows/uwp/monetize/update-an-app-submission) Microsoft Store Submission API.

**Required inputs:**
- AppID
- UpdatedSubmission \<PSObject>

**Returns:** A [submission](https://docs.microsoft.com/en-us/windows/uwp/monetize/manage-app-submissions#app-submission-object) object \<PSCustomObject>

</dd></dl>

### Set-SubmissionPackage

<dl><dd>

**Aliases:** Upload-ApplicationSubmissionPackage, Upload-SubmissionPackage

Uploads the package content (submission .zip) to the URL provided after calling New-ApplicationSubmission.

**Required inputs:**
- PackagePath
- UploadUrl

</dd></dl>

### Stop-ApplicationSubmissionPackageRollout

<dl><dd>

Stops the package rollout for the specified application submission.

All users will now begin receiving the fallback submission.

Wraps the [Halt Package Rollout](https://docs.microsoft.com/en-us/windows/uwp/monetize/halt-the-package-rollout-for-an-app-submission) Microsoft Store Submission API.

**Required inputs:**
- AppId
- SubmissionId

**Returns:** A [Package Rollout](https://docs.microsoft.com/en-us/windows/uwp/monetize/manage-app-submissions#package-rollout-object) object \<PSCustomObject>

</dd></dl>

### Update-ApplicationSubmission

<dl><dd>

Creates a new submission for an existing application on the developer account by
cloning the existing submission and modifying specific parts of it. The
parts that will be modified depend solely on the switches that are passed in.

This is a high-level method that wraps other submission-related methods:
- New-ApplicationSubmission
- Set-ApplicationSubmission
- Set-SubmissionPackage
- Complete-ApplicationSubmission

This app must already have at least one *published* submission completed via
the website in order for this function to work.
You cannot submit a new application submission if there is an existing pending
application submission for $AppId already.  You can use -Force to work around this.

**Required inputs:**
- AppId
- SubmissionDataPath

**Returns:** Array containing:
- The id for the new pending submission.
- The URL that the package needs to be uploaded to.

</dd></dl>

-----
## Working with Application Flight Submissions

### Complete-ApplicationFlightSubmission

<dl><dd>
</dd></dl>

### Complete-ApplicationFlightSubmissionPackageRollout

<dl><dd>
</dd></dl>

### Get-ApplicationFlightSubmission

<dl><dd>
</dd></dl>

### Get-ApplicationFlightSubmissionPackageRollout

<dl><dd>
</dd></dl>

### Get-ApplicationFlightSubmissionStatus

<dl><dd>
</dd></dl>

### New-ApplicationFlightSubmission

<dl><dd>
</dd></dl>

### Remove-ApplicationFlightSubmission

<dl><dd>
</dd></dl>

### Set-ApplicationFlightSubmission

<dl><dd>
</dd></dl>

### Stop-ApplicationFlightSubmissionPackageRollout

<dl><dd>
</dd></dl>

### Update-ApplicationFlightSubmission

<dl><dd>
</dd></dl>


-----
## Working with In-App Product Submissions

<dl><dd>
</dd></dl>

### Complete-InAppProductSubmission

<dl><dd>
</dd></dl>

### Get-InAppProductSubmission

<dl><dd>
</dd></dl>

### Get-InAppProductSubmissionStatus

<dl><dd>
</dd></dl>

### New-InAppProductSubmission

<dl><dd>
</dd></dl>

### New-InAppProductSubmissionPackage

<dl><dd>
</dd></dl>

### New-StoreBrokerInAppProductConfigFile

<dl><dd>
</dd></dl>

### Remove-InAppProductSubmission

<dl><dd>
</dd></dl>

### Set-InAppProductSubmission

<dl><dd>
</dd></dl>

### Update-InAppProductSubmission

<dl><dd>
</dd></dl>


-----
## Utility: Account Interaction

### Clear-StoreBrokerAuthentication

<dl><dd>
</dd></dl>

### Set-StoreBrokerAuthentication

<dl><dd>
</dd></dl>


-----
## Utility: User Interaction

### Format-Application

<dl><dd>
</dd></dl>

### Format-ApplicationFlight

<dl><dd>
</dd></dl>

### Format-ApplicationFlightSubmission

<dl><dd>
</dd></dl>

### Format-ApplicationFlights

<dl><dd>
</dd></dl>

### Format-ApplicationInAppProducts

<dl><dd>
</dd></dl>

### Format-ApplicationSubmission

<dl><dd>
</dd></dl>

### Format-Applications

<dl><dd>
</dd></dl>

### Format-InAppProduct

<dl><dd>
</dd></dl>

### Format-InAppProductSubmission

<dl><dd>
</dd></dl>

### Format-InAppProducts

<dl><dd>
</dd></dl>

### Open-DevPortal

<dl><dd>
</dd></dl>

### Open-Store

<dl><dd>
</dd></dl>

### Start-ApplicationFlightSubmissionMonitor

<dl><dd>
</dd></dl>

### Start-InAppProductSubmissionMonitor

<dl><dd>
</dd></dl>

### Start-SubmissionMonitor

<dl><dd>
</dd></dl>

### Update-ApplicationFlightSubmissionPackageRollout

<dl><dd>
</dd></dl>

### Update-ApplicationSubmissionPackageRollout

<dl><dd>
</dd></dl>


-----
## Utility: Other

### Invoke-SBRestMethod

<dl><dd>
</dd></dl>

### Invoke-SBRestMethodMultipleResult

<dl><dd>
</dd></dl>

