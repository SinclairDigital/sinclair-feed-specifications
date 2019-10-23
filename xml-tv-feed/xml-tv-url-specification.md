# Feed Urls for XML TV

Feed URLs needs to follow a particular format so that the schedule can be retrieved for a specified date.

## Preferred Format

The preferred format is to include a query parameter named `date` where the date is specified as `YYYY-MM-DD`.

Example: `https://www.example.org/feed.xml?date=2019-09-14`

## Alternate Format (deprecated)

An alternate format is also supported where the date can be specified within the path. The date needs to be specified as `YYYY-MM-DD`.

Example: `https://www.example.org/feed2019-09-14.xml`
