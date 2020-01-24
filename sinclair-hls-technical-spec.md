# Sinclair HLS Technical Specification

## HLS Specification

The HLS specification is a published RFC [RFC8216](https://tools.ietf.org/html/rfc8216).

### HLS Protocol Version
Currently, HLS protocol version 6 is supported by Sinclair.

### HTTPS Protocol
Sinclair currently does not support playback of media playlists using HTTP protocol. Thus HTTPS protocol is required for all media playlists from all content providers. Self signed certificates are not accepted.

URIs of media playlists and media segments must conform to Uniform Resource Identifier (URI): Generic Syntax [RFC3986](https://tools.ietf.org/html/rfc3986). Specifically, if data for a URI component would conflict with a reserved character's purpose as a delimiter, then the conflicting data must be percent-encoded before the URI is formed. Nonconforming media playlists will have various difficulties playing on end users' devices.

### Cross-Origin Resource Sharing (CORS)
Content providers must support [CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS) as modern browsers will prevent playback of the content from third party websites if CORS is not enabled.
 
 Sample CORS headers in HTTPS responses:
```
access-control-allow-credentials: true
access-control-allow-headers: Authorization
access-control-allow-origin: https://stirr.com
```

### HLS Authoring Specification for Apple Devices
Content providers are encouraged to refer to [Apple HLS Authoring Specification](https://developer.apple.com/documentation/http_live_streaming/hls_authoring_specification_for_apple_devices) for best viewer experiences on Apple devices.

#### Media Segmentation
Target durations SHOULD be 6 seconds.

Example manifest:
```
#EXTM3U
#EXT-X-VERSION:6
#EXT-X-TARGETDURATION:6
```
Media segments MUST NOT exceed 2 times of the specified target duration. Media segments with durations more than 12 seconds will have various difficulties playing on end users' devices.

#### Support of EXT-X-BYTERANGE Tag
Sinclair currently does not support using of EXT-X-BYTERANGE tag in HLS manifests. Presence of EXT-X-BYTERANGE tag in HLS manifests will cause the player to download the same video every time before playback can start.

#### Media Sequence Number
The media sequence number of the newly refreshed playlist compared to last playlist MUST NOT increase by more than the number of new media segments appended to the new playlist. This is vital as any discrepancy will cause the playback to stall on end users' devices.

### HLS AES Encryption
Only AES-128 and NONE methods for content encryption are supported for retransmission. SAMPLE-AES and fragmented MP4(fMP4) container are not supported at this time.

### HLS Validation
Content providers are encouraged to use **Media Stream Validator** (`mediastreamvalidator`) to simulate a HTTP Live Streaming session and verify that the index file and media segments conform to the HTTP Live Streaming specification. This tool can validate both local files and HTTPS URLs. Download link can be located at the [Resources](#Resources) section below.

## Recommended Video Formats

Our goal is for you to have the highest quality version of your video library to work with.

"Preferred" indicates our **recommended** formats, it’s best if you meet or exceed these levels.
"Supported" indicates the **minimum** supported formats.  Video files that do not meet these levels may have noticeable quality issues when your programming airs.

| Content Format           | Description
|--------------------------|----------------------------------------------------------------------------
| Video                    | MP4 or MOV container. Preferred: HD 1080p, h.264, High profile, 4.1. Supported: HD 720p, h.264, Main profile, 3.0. No Edit Lists, Closed GOP, 1 second long, Chroma subsampling: 4:2:0
| Aspect Ratio (16:9)      | Preferred: 16:9, 1920x1080. Supported: 16:9, 1280x720. Sinclair distributes to 16:9 aspect ratio players. Other aspect ratios will be processed and  black bars will be added on the left/right (pillar boxes) or at the top/bottom (letter boxes) to make a 16:9 ratio on playout
| Video Frame Rate         | Preferred: 29.97 fps or 30 fps. Supported: 23.98, 24, 25, 30, 48, 50, 60 fps. Keep the frame rate in the format in which it was recorded. Interlaced content must be deinterlaced
| Video Bit Rate           | Preferred: 1080p at 15 mbps (or higher), 720p at 9.5 mbps (or higher). Supported: 1080p at 6 mbps, 720p at 3 mbps
| Audio                    | Preferred:  AAC, AAC-LC. Supported:  PCM 16-bit. All content must have an audio track.
| Audio Setting            | 2-channel stereo
| Audio Sample Rate        | Preferred:  48 Khz. Supported:  44.1 Khz.
| Audio Bit Rate           | Preferred: Stereo at 384kbps. Supported: Stereo at 128kbps (or higher)
| Audio Level              | All audio levels must be below 0db. Overall audio level should normalized to -24db.
| Closed Captioning        | Closed captioning should be embedded according to [EIA-608](https://en.wikipedia.org/wiki/EIA-608) or [EIA-708](https://ecfsapi.fcc.gov/file/6511959011.pdf)
| Ad Marking               | Ad markers should be included according to [SCTE-35](https://dev.scte.org/SCTEDocs/Standards/SCTE%2035%202019.pdf). At minimum `EXT-CUE-IN` and `EXT-CUE-OUT` markers are expected

## Playlist Examples
### Master Playlist Example
Sinclair currently uses a naming convention by specifying the variant streams as B, C, D, E, F, G variant, with bitrates starting from the lowest bitrate (B variant) to the highest bitrate (G variant). Although the naming convention is not part of the specification, content providers are encouraged to use the same naming conventions to facilitate easier troubleshooting of playback issues.
```
#EXTM3U
#EXT-X-VERSION:6
#EXT-X-INDEPENDENT-SEGMENTS
#EXT-X-MEDIA:TYPE=AUDIO,GROUP-ID="aac",NAME="English",LANGUAGE="en",AUTOSELECT=YES,DEFAULT=YES
#EXT-X-MEDIA:TYPE=CLOSED-CAPTIONS,NAME="English",AUTOSELECT=YES,DEFAULT=YES,LANGUAGE="en",INSTREAM-ID="CC1",GROUP-ID="ccs"
#EXT-X-STREAM-INF:RESOLUTION=416x234,BANDWIDTH=445125,CODECS="mp4a.40.5,avc1.42000d",FRAME-RATE=30.000,AUDIO="aac",CLOSED-CAPTIONS="ccs",AVERAGE-BANDWIDTH=421365
d.m3u8
#EXT-X-STREAM-INF:RESOLUTION=704x396,BANDWIDTH=745125,CODECS="mp4a.40.5,avc1.4d001e",FRAME-RATE=30.000,AUDIO="aac",CLOSED-CAPTIONS="ccs",AVERAGE-BANDWIDTH=714177
e.m3u8
#EXT-X-STREAM-INF:RESOLUTION=896x504,BANDWIDTH=1291125,CODECS="mp4a.40.5,avc1.4d001f",FRAME-RATE=30.000,AUDIO="aac",CLOSED-CAPTIONS="ccs",AVERAGE-BANDWIDTH=1240311
f.m3u8
#EXT-X-STREAM-INF:RESOLUTION=1280x720,BANDWIDTH=2689125,CODECS="mp4a.40.5,avc1.4d001f",FRAME-RATE=30.000,AUDIO="aac",CLOSED-CAPTIONS="ccs",AVERAGE-BANDWIDTH=2598547
g.m3u8
#EXT-X-STREAM-INF:RESOLUTION=192x108,BANDWIDTH=136451,CODECS="mp4a.40.5,avc1.42000b",FRAME-RATE=15.000,AUDIO="aac",CLOSED-CAPTIONS="ccs",AVERAGE-BANDWIDTH=121335
b.m3u8
#EXT-X-STREAM-INF:RESOLUTION=256x144,BANDWIDTH=247125,CODECS="mp4a.40.5,avc1.42000c",FRAME-RATE=30.000,AUDIO="aac",CLOSED-CAPTIONS="ccs",AVERAGE-BANDWIDTH=236437
c.m3u8
```
#### Variant Playlist Example
An example of G variant playlist is shown below. The media segment file names use Sinclair naming convention and start with G.
```
#EXTM3U
#EXT-X-VERSION:6
#EXT-X-MEDIA-SEQUENCE:42790
#EXT-X-TARGETDURATION:6
#EXT-X-KEY:METHOD=AES-128,URI="https://content-ausw5.uplynk.com/check2?b=d0dcee9d692940b5ac86b9c772af2d74&v=3e45c6b5354a40f787e0b2aadb0f5d6a&r=g&c=3e45c6b5354a40f787e0b2aadb0f5d6a&pbs=7c166d00f9634172b8c5dfb5eda64f2d",IV=0x000000000000000000000000000000A8
#EXTINF:4.0960,
https://x-default-stgec.uplynk.com/ause/slices/d0d/34d28c6069b34f1d96307c80809697d7/d0dcee9d692940b5ac86b9c772af2d74/G000000A8.ts?pbs=7c166d00f9634172b8c5dfb5eda64f2d&_jt=l&chid=3e45c6b5354a40f787e0b2aadb0f5d6a&si=41
#EXT-X-KEY:METHOD=AES-128,URI="https://content-ausw5.uplynk.com/check2?b=d0dcee9d692940b5ac86b9c772af2d74&v=3e45c6b5354a40f787e0b2aadb0f5d6a&r=g&c=3e45c6b5354a40f787e0b2aadb0f5d6a&pbs=7c166d00f9634172b8c5dfb5eda64f2d",IV=0x000000000000000000000000000000A9
#EXTINF:4.0960,
https://x-default-stgec.uplynk.com/ause/slices/d0d/34d28c6069b34f1d96307c80809697d7/d0dcee9d692940b5ac86b9c772af2d74/G000000A9.ts?pbs=7c166d00f9634172b8c5dfb5eda64f2d&_jt=l&chid=3e45c6b5354a40f787e0b2aadb0f5d6a&si=41
#EXT-X-KEY:METHOD=AES-128,URI="https://content-ausw5.uplynk.com/check2?b=d0dcee9d692940b5ac86b9c772af2d74&v=3e45c6b5354a40f787e0b2aadb0f5d6a&r=g&c=3e45c6b5354a40f787e0b2aadb0f5d6a&pbs=7c166d00f9634172b8c5dfb5eda64f2d",IV=0x000000000000000000000000000000AA
#EXTINF:4.0960,
https://x-default-stgec.uplynk.com/ause/slices/d0d/34d28c6069b34f1d96307c80809697d7/d0dcee9d692940b5ac86b9c772af2d74/G000000AA.ts?pbs=7c166d00f9634172b8c5dfb5eda64f2d&_jt=l&chid=3e45c6b5354a40f787e0b2aadb0f5d6a&si=41
#EXT-X-KEY:METHOD=AES-128,URI="https://content-ausw5.uplynk.com/check2?b=d0dcee9d692940b5ac86b9c772af2d74&v=3e45c6b5354a40f787e0b2aadb0f5d6a&r=g&c=3e45c6b5354a40f787e0b2aadb0f5d6a&pbs=7c166d00f9634172b8c5dfb5eda64f2d",IV=0x000000000000000000000000000000AB
#EXTINF:4.0960,
https://x-default-stgec.uplynk.com/ause/slices/d0d/34d28c6069b34f1d96307c80809697d7/d0dcee9d692940b5ac86b9c772af2d74/G000000AB.ts?pbs=7c166d00f9634172b8c5dfb5eda64f2d&_jt=l&chid=3e45c6b5354a40f787e0b2aadb0f5d6a&si=41
#EXT-X-KEY:METHOD=AES-128,URI="https://content-ausw5.uplynk.com/check2?b=d0dcee9d692940b5ac86b9c772af2d74&v=3e45c6b5354a40f787e0b2aadb0f5d6a&r=g&c=3e45c6b5354a40f787e0b2aadb0f5d6a&pbs=7c166d00f9634172b8c5dfb5eda64f2d",IV=0x000000000000000000000000000000AC
#EXTINF:4.0960,
https://x-default-stgec.uplynk.com/ause/slices/d0d/34d28c6069b34f1d96307c80809697d7/d0dcee9d692940b5ac86b9c772af2d74/G000000AC.ts?pbs=7c166d00f9634172b8c5dfb5eda64f2d&_jt=l&chid=3e45c6b5354a40f787e0b2aadb0f5d6a&si=41
#EXT-X-KEY:METHOD=AES-128,URI="https://content-ausw5.uplynk.com/check2?b=d0dcee9d692940b5ac86b9c772af2d74&v=3e45c6b5354a40f787e0b2aadb0f5d6a&r=g&c=3e45c6b5354a40f787e0b2aadb0f5d6a&pbs=7c166d00f9634172b8c5dfb5eda64f2d",IV=0x000000000000000000000000000000AD
#EXTINF:4.0960,
https://x-default-stgec.uplynk.com/ause/slices/d0d/34d28c6069b34f1d96307c80809697d7/d0dcee9d692940b5ac86b9c772af2d74/G000000AD.ts?pbs=7c166d00f9634172b8c5dfb5eda64f2d&_jt=l&chid=3e45c6b5354a40f787e0b2aadb0f5d6a&si=41
```

## Resources

[Apple's HTTP Live Streaming Tools](https://developer.apple.com/documentation/http_live_streaming/about_apple_s_http_live_streaming_tools)
