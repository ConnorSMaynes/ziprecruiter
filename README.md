

<p align="left">
<img src="https://github.com/ConnorSMaynes/ziprecruiter/blob/master/ziprecruiter/static/logo.png" alt="ZipRecruiter Bot" >
</p>

A simple unofficial api for ziprecruiter.

<p align="left">
<img src="https://github.com/ConnorSMaynes/ziprecruiter/blob/master/ziprecruiter/static/batteries.png", alt="Batteries Included - Selenium - Chrome Webdriver" width=30, height=30>
      Selenium Batteries Included - Chrome Webdriver
</p>

## Methods

- `login` : Login to ZipRecruiter with the provided credentials. ZipRecruiter is protected by No Captcha ReCaptcha, so if this pops up and login cannot proceed the selenium browser will restart and display itself so you can solve the captcha. Selenium is ONLY used for login, because of the captcha problem, everything else is nice and fast through requests.
- `search` : search for jobs. returns a list of search results named tuples with ApplyLink ( quick apply job link ) and DetailsLink ( link to job desciption and other job details ). generator. The following filters are supported:
  - keywords
  - posted x days ago
  - salary
  - type ( full-time, internship, temporary )
- `uploadResume` : Upload the provided resume to ziprecruiter to replace the existing resume in the account.
- `apply` : apply to the job at the given url ( ApplyLink ) returned from `search`
- `batchApply` : apply to a bunch of jobs at once. progress bar.
- `getApplied` : get json/dict of data about jobs applied to
- `getJobDetails` : get details on a given job from the DetailsLink of the search result returned from `search`

## Installation

```bash
pip install git+git://github.com/ConnorSMaynes/ziprecruiter
```

## Usage

```python
from ziprecruiter.ziprecruiter import ZipRecruiter

# LOGIN
z = ZipRecruiter()
z.login( USERNAME, PASSWORD )

# UPLOAD LATEST RESUME
z.uploadResume( FilePath=RESUME_FILE_PATH )

# BATCH APPLY TO JOBS
Jobs = list( z.search( Quantity=5, keywords='developer' ) )
z.batchApply( Jobs )                                        # apply to a bunch of jobs with progress bar.

# GET DETAILS ON LAST FEW JOBS APPLIED TO
LastJobsAppliedTo = z.getApplied( 5 )                       # get last 5 jobs applied to

# APPLY TO JOBS AND GET DETAILS
Jobs = z.search( Quantity=5, keywords='developer' )
for Job in Jobs:                                            # apply to jobs and do some other stuff
    JobDetails = z.getJobDetails( Job.DetailsLink )         # note how we access the DetailsLink and ApplyLink
    AppResult = z.apply( Job.ApplyLink )
    if AppResult:
        print( JobDetails )
```

## Similar Projects

This project was inspired by others:
- [getJob](https://github.com/jonathanhwinter/getJob)
- [ZipRecruiterHack](https://github.com/Original-heapsters/ZipRecruiterHack)

## License

Copyright © 2018, [ConnorSMaynes](https://github.com/ConnorSMaynes). Released under the [MIT](https://github.com/ConnorSMaynes/ziprecruiter/blob/master/LICENSE).

