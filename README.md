# Sinclair External Ingest Specification
This is the documentation for providing linear feeds and VOD to the Sinclair Broadcast Group Digital Platform.

## Linear Feeds
Linear feeds are specified by two files which must be available from a public URL:

### Linear HLS Manifest
Linear feeds require an HLS Stream with SCTE-35 Ad markers and embedded 608 Closed Captions. Addition technical requirements may be found in our [HLS Technical Spec](sinclair-hls-technical-spec.md)

### Program Schedule 
Program schedules must be specified according to our [External Linear Feed Spec](sinclair-linear-feed-spec.md)

## VOD Feeds
VOD feeds are specified by one main structural file and a series of streams for content.

### VOD Structure Feed
VOD feeds are embodied by a publically-available JSON file which must adhere to our [External VOD Feed Spec](sinclair-vod-feed-spec.md). This feed must include links to HLS manifest files for each video item.

### VOD HLS Manifest
VOD items (movies, episodes, etc...) require an HLS Stream with embedded 608 Closed Captions. Ads may be specified as SCTE-35 Ad markers or included in the VOD Structure Feed as described by the spec. Addition technical requirements may be found in our [HLS Technical Spec](sinclair-hls-technical-spec.md)
