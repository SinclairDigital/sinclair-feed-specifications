# Sinclair External Linear Feed

### Overview

This guide includes detailed information on the Sinclair External Linear Feed Specification, which can be used to build a content feed of linear video content. This schema conforms to the TIVO/Rovi XML Schema for program scheduling ([XSD](rovi-docs-and-xml/RoviExternalListings.xsd) [Data Types](rovi-docs-and-xml/RoviExternalListingsDataTypes.xsd))

**Sections:**
* [Linear Feed Schema](#linear-feed-schema)

**Content types:**
* [Rovi_Listings](#rovilistings)
  * [Programs](#programs)
* [EventRatingTypeDef](#eventratingtypedef)
  * [EventRating](#eventrating)
* [PgmRatingTypeDef](#pgmratingtypedef)
  * [PgmRating](#pgmrating)
* [RatingReasons](#ratingreasons)
  * [RatingReason](#ratingreason)
* [GenreTypeDef](#genretypedef)
  * [Genre](#genre)
* [CreditsTypeDef](#creditstypedef)
  * [Credit](#credit)
* [UGCSTypeDef](#ugcstypedef)
* [ProgramCopyTypeDef](#programcopytypedef)
  * [PgmDescription](#pgmdescription)
* [ScheduleTypeDef](#scheduletypedef)
  * [Schedule](#schedule)
* [ProgramTypeDef](#programtypedef)
  * [AlternateTitles](#alternatetitles)
    * [Title](#title)
  * [RichMedia](#richmedia)
    * [Images](#images)
      * [Image](#image)
        * [Rights](#rights)
          * [Right](#right)
* [MiscAttributes](#miscattributes)
  * [Attribute](#attribute)
* [CaptionDataType](#captiondatatype)
* [AiringDataType](#airingdatatype)
* [PgmColorDataType](#pgmcolordatatype)
* [ShowingDataType](#showingdatatype)
* [AudioLevelDataType](#audioleveldatatype)
* [HDTVLevelDataType](#hdtvleveldatatype)
* [AlternateTitleTypeDataType](#alternatetitletypedatatype)
* [CategoryDataType](#categorydatatype)
* [ProgramTypeDataType](#programtypedatatype)
* [CreditDataType](#creditdatatype)
* [GenreDataType](#genredatatype)
* [PgmRatingTypeDataType](#pgmratingtypedatatype)
* [PgmRatingDataType](#pgmratingdatatype)
* [EventRatingTypeDataType](#eventratingtypedatatype)
* [EventRatingDataType](#eventratingdatatype)
* [StarRatingDataType](#starratingdatatype)
* [AspectRatioDataType](#aspectratiodatatype)
* [ThreeDFormatDataType](#threedformatdatatype)
* [SourceRegionDataType](#sourceregiondatatype)
* [ImageTypeDataType](#imagetypedatatype)
* [ImageFileFormatDataType](#imagefileformatdatatype)

---

## Linear Feed Schema
These are the properties for the root object of your feed.

| Field | Type | Required | Description |
| ----- | ---- | -------- | ----------- |
| Rovi_Listings | [Rovi_Listings Object](#rovilistings) | Required | 

---

## Rovi_Listings
| Field | Type | Required | Description |
| ----- | ---- | -------- | ----------- |
| Programs | [Programs Object](#programs) | Optional | Program metadata for this event.
| SourceRegion | [SourceRegionDataType enum](#sourceregiondatatype) | Optional | Indentifies the region of Station. Currently Ingest primarily recognizes region as either 'North America' (default) or 'Europe'
| Station | string | Optional | 

## Programs
| Field | Type | Required | Description |
| ----- | ---- | -------- | ----------- |
| Program | list of [ProgramTypeDef Object](#programtypedef) | Optional | Program metadata for this event.

## EventRatingTypeDef
| Field | Type | Required | Description |
| ----- | ---- | -------- | ----------- |
| EventRating | [EventRating Object](#eventrating) | Optional | All ratings for the individual program.

## EventRating
| Field | Type | Required | Description |
| ----- | ---- | -------- | ----------- |
| RatingReasons | [RatingReasons Object](#ratingreasons) | Optional | Reasons for the rating applied to the program.
| Type | [EventRatingTypeDataType Object](#eventratingtypedatatype) | Optional | The name or acronym of the agency that has rated this program.
| TVRating | [EventRatingDataType Object](#eventratingdatatype) | Optional | This field is used to specify the Rating of the program.

## PgmRatingTypeDef
| Field | Type | Required | Description |
| ----- | ---- | -------- | ----------- |
| PgmRating | [PgmRating](#pgmrating) | Optional | 

## PgmRating
| Field | Type | Required | Description |
| ----- | ---- | -------- | ----------- |
| RatingReasons | [RatingReasons Object](#ratingreasons) | Optional | Reasons for the rating applied to the program.
| Type | [PgmRatingTypeDataType Object](#pgmratingtypedatatype) | Optional | The name or acronym of the agency that has rated this program.
| Rating | [PgmRatingDataType Object](#pgmratingdatatype) | Optional | This field is used to specify the Rating of the program.

## RatingReasons
| Field | Type | Required | Description |
| ----- | ---- | -------- | ----------- |
| RatingReason | [RatingReason Object](#ratingreason) | Optional | 

## RatingReason
| Field | Type | Required | Description |
| ----- | ---- | -------- | ----------- |
| value | string | Required | 

## GenreTypeDef
| Field | Type | Required | Description |
| ----- | ---- | -------- | ----------- |
| Genre | [Genre Object](#genre) | Optional | 

## Genre
| Field | Type | Required | Description |
| ----- | ---- | -------- | ----------- |
| value | [GenreDataType object](#genredatatype) | Optional | A single genre entry.

## CreditsTypeDef
| Field | Type | Required | Description |
| ----- | ---- | -------- | ----------- |
| Credit | [Credit Object](#credit) | Optional | At least one Credit Type of ‘Actor’ must be provided when the program type has been designated as ‘Movie’.  The credit sequence attribute is MANDATORY only when credit information is provided for the program.

## Credit
| Field | Type | Required | Description |
| ----- | ---- | -------- | ----------- |
| Type | [CreditDataType Object](#creditdatatype) | Optional | Used to designate actors and other persons affiliated with a program.  (e.g., actor, director, narrator, host, etc.) Each Credit Type entry must have an associated Credit Name.
| Name | string | Optional | The actual name of the actor or other persons affiliated with a program. (e.g., Tom Hanks, Robert Redford)  Each Credit Name entry must have an associated Credit Type. 
| Role | string | Optional | The role played by an actor.  (e.g., Rhett Butler)  Each Role entry must have an associated Credit Name and Credit Type.
| Language | string | Optional | Used to describe Language the credit text is in.
| Sequence | nonNegativeInteger | Optional | When more than one credit is provided for a program, this attribute will prioritize the display sequence of the credits to the end-user.  When provided, the credit sequence of a program should be a non-negative integer value.
| RoviCreditID | nonNegativeInteger | Optional | A credit ID corresponds to ROVI Credit IDs, used when partner can send pre-matched Credits to ROVI as determined by ROVI.

## UGCSTypeDef
| Field | Type | Required | Description |
| ----- | ---- | -------- | ----------- |
| Category | string | Optional | 
| Type | string | Optional | 
| Content | string | Optional | 

## ProgramCopyTypeDef
| Field | Type | Required | Description |
| ----- | ---- | -------- | ----------- |
| PgmDescription | [PgmDescription Object](#pgmdescription) | Optional | Valid program descriptions.

## PgmDescription
| Field | Type | Required | Description |
| ----- | ---- | -------- | ----------- |
| AffiliateStation | string | Optional | Not used at this time. Consult with Rovi representative before using it in Program Description.
| Type | string | Optional | 
| Description | string | Optional | Description of the program. Length limits as per determined by Description type (refer Guide book)
| Culture | string | Optional | Determines the culture of program description text.

## ScheduleTypeDef
| Field | Type | Required | Description |
| ----- | ---- | -------- | ----------- |
| Schedule | [Schedule Object](#schedule) | Optional | 

## Schedule
| Field | Type | Required | Description |
| ----- | ---- | -------- | ----------- |
| Ratings | [EventRatingTypeDef Object](#eventratingtypedef) | Optional | All ratings for the individual airing.
| MiscAttributes | [MiscAttributes Object](#miscattributes) | Optional | 
| AffiliateStation | string | Optional | The Source ID is the unique ID that represents the source (station).
| TimeZone | string | Optional | This is the time zone in which the calendar date and broadcast time of a program is being provided.
| CalendarDT | dateTime | Optional | This is the calendar date and time of the program.
| StartTime | string | Optional | The start time of the program.  If the CalendarDT does not contain the start time this attribute must be populated.
| EndTime | string | Optional | The end time of the program.  This attribute is optional if the duration is provided.
| Duration | nonNegativeInteger | Optional | This is the duration of the program being aired, in minutes.  This attribute is not required if the end time is provided.
| AssetID | string | Optional | A numeric value designated to point to a schedule that is non linear- VOD
| ShowingType | ShowingDataType | Optional | Showing type of the program.
| AspectRatio | AspectRatioDataType | Optional | The Width and Height ratio of the onscreen program being broadcasted
| SAP | boolean | Optional | Designates programs broadcasted with narrated descriptions for visually impaired
| Subtitled | boolean | Optional | Designate whether the program has subtitles on screen.
| SubtitleLanguage | string | Optional | Indicates the language in which the program is subtitled, if applicable.
| UmbrellaTitle | string | Optional | The Umbrella Title gives the option to override the program title in the schedule
| PartNumber | nonNegativeInteger | Optional | Indicates the part number. Used only on long programs such as movies that are airing in multiple parts.  If this field is provided, Part Total must also be provided.
| PartTotal | nonNegativeInteger | Optional | Indicates the total number of parts. Used only on long programs such as movies that are airing n multiple parts.  Required if Part Number is provided.
| PgmColorType | PgmColorDataType | Optional | Denotes the color of the program being broadcast.
| Caption | CaptionDataType | Optional | Caption feature of the program.
| AiringType | AiringDataType | Optional | Airing type of the program.
| AudioLevel | AudioLevelDataType | Optional | Indicates the Audio level of the program.  Indicate actual level (Dolby Digital, Dolby 5.1, etc.) if known, "Stereo" if the if the exact level is unknown, or "None" if this program is not being aired in Stereo.
| HDTVLevel | HDTVLevelDataType | Optional | Indicates the level of high definition of the program.  Indicate actual level (720p, 1081I, etc.) if known, "HD" if the if the exact level is unknown, or "None" if this program is not being aired in HD.
| DVI | boolean | Optional | Designates programs broadcast with narrated descriptions for the visually impaired
| JoinedInProgress | boolean | Optional | Use if the program start time is delayed
| SubjectToBlackout | boolean | Optional | If the program is locally subjected to blackout
| Dubbed | string | Optional | Indicates the language in which the program is dubbed.
| IsEncrypted | boolean | Optional | Designate whether the program is encrypted.
| VPS | dateTime | Optional | International attribute for Video Programming Service VPS and PDC systems are used by many analogue TV stations to ensure that a timer recording catches the whole programme even when the programme is not running to schedule.This means that if you input the announced time and date of the programme that you want to record, and that programme happens to run late, for example, VPS and PDC will automatically correct the timed recording on your recorder. 
| Highlight | string | Optional | International field, specific highlights for the broadcast.
| BroadcastLanguage | string | Optional | The Language the program is being broadcast in. Only to be used in cases where the original Language is different
| StarRating | StarRatingDataType | Optional | 
| ThreeDFormat | ThreeDFormatDataType | Optional | 

## ProgramTypeDef
| Field | Type | Required | Description |
| ----- | ---- | -------- | ----------- |
| Genres | GenreTypeDef | Optional | A list of descriptive words that may be assigned to help identify and categorize the content of the program, helping users get more information about the exact content of the program.
| Ratings | PgmRatingTypeDef | Optional | All ratings for the program.
| Credits | CreditsTypeDef | Optional | All credits for the program.
| UGCS | UGCSTypeDef | Optional | EU program classification data. International third party classification, Universal Genre Classification System
| PgmDescriptions | ProgramCopyTypeDef | Optional | All descriptions for the program.
| AlternateTitles | [AlternateTitles Object](#alternatetitles) | Optional | 
| RichMedia | [RichMedia Object](#richmedia) | Optional | 
| MiscAttributes | [MiscAttributes Object](#miscattributes) | Optional | 
| Schedules | ScheduleTypeDef | Optional | An individual event in the source's schedule.
| StationProgramID | string | Optional | Uniquely identifies a single program. This can be either a number or alphanumeric code, must uniquely identify a single program, and be guaranteed not to change or to be re-used.
| ProgramType | ProgramTypeDataType | Optional | 
| Category | CategoryDataType | Optional | The single most appropriate categorization for this program outside of ProgramType.
| ProgramTitle | string | Optional | Full title by which this program is commonly known.
| OriginalTitle | string | Optional | The title under which the program was first released by the production company or the producing TV source. Please fill in these fields whenever you can confirm them.
| OriginalAirDate | dateTime | Optional | Original date that the program aired on this source. MMDDYYYY format.
| OriginalContent | string | Optional | Is the program original to this network (Y/N).
| SeriesEpisodeTitle | string | Optional | Episode Title, as supplied by the distributor or syndicator.  Either this field, Episode Number or Part Number must be provided for Series Episodes.
| OriginalEpisodeTitle | string | Optional | The Episode title under which the program was first released by the production company or the producing TV source. Please fill in these fields whenever you can confirm them.
| SeriesEpisodeNumber | string | Optional | Episode Number, as supplied by the distributor or syndicator.  Either this field, Episode Title or Part Number must be provided for Series Episodes.
| SeriesId | string | Optional | 
| SeriesSeasonNumber | string | Optional | An integer value that identifies the season that the program was created/aired.
| YearOfRelease | int | Optional | The year the program/version was released in YYYY format.  Required for movies, but is optional for other program types.
| Runtime | int | Optional | The runtime is the length/duration of the program. This value shall be provided in minutes.
| PrimaryLanguage | string | Optional | Indicates the primary language in which the program was created.
| OriginalTitleLanguage | string | Optional | To be used if the program language and the broadcasting language is different
| CountryOfOrigin | string | Optional | Identifies the country where the program was originally produced.
| ProdCompany | string | Optional | The company that produced the program.
| DistName | string | Optional | The company that syndicates/distributes the program, if applicable.
| NOLAcode | string | Optional | 
| SportsLeague | string | Optional | Official League Name for this event.  E.g., NFL, AFL, MLB, etc.
| SportsTeam1 | string | Optional | Generally indicates the home team, when event is not being aired at a neutral site.  This field may be blank for non-team events.
| SportsTeam2 | string | Optional | Generally indicates the away team, when event is not being aired at a neutral site.  This field may be blank for non-team events.
| SportsEventDate | dateTime | Optional | Specifies the actual date on which the sporting event will occur, has occurred.
| PartNumber | nonNegativeInteger | Optional | Indicates the part number of a multi-part movie, episode or special.  If this field is provided, Part Total must also be provided.
| PartTotal | nonNegativeInteger | Optional | Indicates the total number of parts. (e.g., Part 1 of 2) of a multi-part movie, episode or special.  Required if Part Number is provided.
| PgmColorType | PgmColorDataType | Optional | Denotes the color of the program being broadcast.
| Caption | CaptionDataType | Optional | Identifies the type of captioning that is available on the program.
| AiringType | AiringDataType | Optional | 
| AudioLevel | AudioLevelDataType | Optional | Indicate actual level (Dolby Digital, Dolby 5.1, etc.) if known; Stereo if the exact level is unknown; or None if this program isn’t broadcast in Stereo.
| HDTVLevel | HDTVLevelDataType | Optional | Indicate the actual level (720p, 1081I, etc.) if known; HD if the exact level is unknown; or None if the program wasn't created in HD.
| DVI | boolean | Optional | Designates programs created with narrated descriptions for the visually impaired
| ThreeDFormat | ThreeDFormatDataType | Optional | The format of the 3-D value for program

## AlternateTitles
| Field | Type | Required | Description |
| ----- | ---- | -------- | ----------- |
| Title | [Title Object](#title) | Optional | 

## Title
| Field | Type | Required | Description |
| ----- | ---- | -------- | ----------- |
| AltTitleType | [AlternateTitleTypeDataType Object](#alternatetitletypedatatype) | Optional | 
| AltTitleText | string | Optional | 
| AltTitleLanguage | string | Optional | 

## RichMedia
| Field | Type | Required | Description |
| ----- | ---- | -------- | ----------- |
|  | [Images Object](#images) | Optional | 

## Images
| Field | Type | Required | Description |
| ----- | ---- | -------- | ----------- |
| Image | [Image Object](#image) | Optional | 
| AssetID | string | Optional | Uniquely identifies a single RichMedia Asset within sender’s database
| Title | string | Optional | Image Title to be used in case different from Program Title
| Type | ImageTypeDataType | Optional | The type or category of the image (e.g., Head Shot: Key) that can help classify images when they are created or edited.
| Language | string | Optional | If Image has text information then Language of the text.
| Caption | string | Optional | A brief description of the image.
| MediaCredit | string | Optional | The media outlet that should be credited with the image.
| ZoomLevel | nonNegativeInteger | Optional | The relative zoom level of the image.
| NumberOfPeople | nonNegativeInteger | Optional | This field represents number of people in the image.
|FileLocation | string | Optional | Refers to the URL if image is available online, or refers to the file path if images are provided in additional compressed file
| FileName | string | Optional | File name (excluding full path) of the image if providing images as compressed zip file.
| FileFormat | [ImageFileFormatDataType Object](#imagefileformatdatatype) | Optional | Format of the file e.g. jpg, jpeg, PNG etc.

## Image
| Field | Type | Required | Description |
| ----- | ---- | -------- | ----------- |
| Rights | [Rights Object](#rights) | Optional | 

## Rights
| Field | Type | Required | Description |
| ----- | ---- | -------- | ----------- |
| Right | [Right Object](#right) | Optional | 

## Right
| Field | Type | Required | Description |
| ----- | ---- | -------- | ----------- |
| Title | string | Optional | Name of the Image Rights. 
| StartDate | date | Optional | Start Date that above mentioned Image Rights on image are owned
| EndDate | date | Optional | Date on which mentioned Image Rights expire



## MiscAttributes
| Field | Type | Required | Description |
| ----- | ---- | -------- | ----------- |
| Attribute | [Attribute Object](#attribute) | Optional | 

## Attribute
| Field | Type | Required | Description |
| ----- | ---- | -------- | ----------- |
| Key | string | Optional | 
| Value | string | Optional | 

## CaptionDataType
A string with a value in the following list:
* CC, OC, SL, OC/SL, CC/SL, None   

## AiringDataType
A string with a value in the following list:
* Live, Taped, Repeat, New, None

## PgmColorDataType
A string with a value in the following list:
* Color, Black and White, Color &amp; BW Episodes, May be colorized, Colorized

## ShowingDataType
A string with a value in the following list:
* Premiere, Series Premiere, Season Premiere, Finale, Series Finale, Season Finale

## AudioLevelDataType
A string with a value in the following list:
* Stereo, DSS (Surround Sound), Dolby 5.1, None

## HDTVLevelDataType
A string with a value in the following list:
* HD Level Unknown, 720p, 1080i, 480p, 1080p, None

## AlternateTitleTypeDataType
A string with a value in the following list:
* Alias, Alias2, Alias3, Alias4, isis_alias_1, isis_alias_2, isis_alias_3, isis_alias_4, Grid, Grid2, On-Screen, Sort, 30 charact. or less, 50 charact. or less, Alt1, Parent, Adult Generic, Full Sports Subtitle, TVG Title, Umbrella Title, Episode Title, AKA Episode Title 1, AKA Episode Title 2

## CategoryDataType
A string with a value in the following list:
* Movie, Sports, Children&apos;s, News, Other, Lifestyle, Music

## ProgramTypeDataType
A string with a value in the following list:
* OTO, Series, Movie

## CreditDataType
A string with a value in the following list:
* Actor, Director, Cinematographer, Producer, Executive Producer, Key Grip, Choreographer, Author, Composer, Host, Musician, Narrator, Photographer, Screenwriter, Sound Effects, Studio, Voice, Writer, Anchor, Speaker, Special Effects, Play-By-Play, Commentator, Reporter, Analyst, Art Director, Costumes, Panelist, Set Design, Sidekick, Performer, Guest, Conductor, Moderator, Reality Cast Member, Subject (person only), Remarks by, Judge, Announcer, Animation, Assoc. Producer, Casting, Co-Producer, Editor, Make Up, Music Director, Production Designer, Stunts, Technical Advisor, Appearing, Animal Actor, Production Company, Co-Executive Producer, Consulting Producer, Supervising Producer, Co-Creator, Creator

## GenreDataType
A string with a value in the following list:
* action/adventure, advice, adult, arts &amp; literature, baseball, basketball, biography, boxing, business &amp; finance, animated, comedy, comedy-drama, crime drama, documentary, drama, educational, ballet, extreme sports, fashion, food, football, game show, golf, health &amp; fitness, history, hobbies &amp; crafts, home &amp; garden, horror, horse racing, hockey, cartoon, christmas, martial arts, music, mystery &amp; suspense, nature, college, olympics, outdoors, pets, politics, public affairs, reality, religion, roller sports, sci-fi, science &amp; technology, shopping, soap opera, soccer, other, sports, talk, tennis, track &amp; field, travel, volleyball, water sports, western, winter sports, pro wrestling, variety, election, animated comedy, ice skating, ice skating (competition), equestrian, teens, fantasy, musical, video games, paranormal, magazine, newscast, filmed on location, audio only, auto info, motor sports, entertainment, awards, concert, music videos, performance, gospel music, government, dog racing, gymnastics, halloween, hanukkah, health, high school, highlights, home projects, hospital, how-to, figure skating, infomercial, instruction, interview, jai alai, jazz, july 4th, children, kwanzaa, labor day, lacrosse, little league, local, magic, marathon, medicine, memorial day, ml king day, mothers day, mystery, new years day, new years eve, newsmagazine, olympic-style, opera, pageant, parade, passover, pilot, playoffs, police, polo, preschool, pro, profile, psychology, puppets, real estate, remake, retrospective, reviews (critics), running, rodeo, romance, rosh hashana, rowing, rugby, satire, science, costumer, senior citizens, sequel, serial, series finale, shooting, silent, sitcom, skiing, softball, spin-off, sports stuff, st patricks day, stand-up comedy, summer olympics, suspense/thriller, table tennis, tabloid, talent contest, taxes, telecourse, thanksgiving, theatre, timely, trains, triathlon, tribute, truck competition, tvg classic, tvgtalk, valentines day, veterans day, war, weightlifting, winter olympics, women, wrestling, yom kippur, family, alternative, bluegrass, blues, cajun/zydeco, contemporary christian, disco &amp; dance, easy listening, ethnic/world music, funk, heavy metal, hip-hop &amp; rap, latin, new age, new wave &amp; punk, pop, r&amp;b, reggae, rock, ska, soul, big band &amp; swing, techno, vocalists, mardi gras, September 11, play, ramadan, special, episode title in copy, fishing, minor league, fencing, hunting, kayaking, in-line skating, handball, luge, yachting, show tunes, soft rock, smooth jazz, water skiing, gay and lesbian, badminton, canoeing, diving, racquetball, squash, swimming, water polo, motorcycle racing, mountain biking, powerboat racing, part info in copy, snowboarding, short subject, snowmobiling, skateboarding, cinco de mayo, bicycle motocross, adventure race, animals, anime, arm wrestling, auto racing, dog show, parenting, curling, drag racing, bobsledding, bullfighting, card game, cheerleading, speedskating, sumo wrestling, surfing, weather, generic source record, skeleton, prequel, 2006 election, technology, 2008 presidential election, pop culture classic, cult classic, chick flick, guy flick, agriculture, all-star, archery, auction, fine arts, adaptation, coming of age, anthology, art, aviation, biathlon, bicycling, pool, black comedy, boating, bodybuilding, bowling, business, circus, classical music, classifieds, collectibles, commentary, computers, country music, courtroom, crafts, cricket, crime, current affairs, dance, debate, debut, docudrama, easter, environment, espionage, fathers day, field hockey, finance, fitness, folk music, full-contact, fundraiser/telethon, gardening, compilation, cooking, ADULT, ARTS &amp; CULTURE, CHILDREN, GENERAL ENTERTAINMENT, HEALTH &amp; FITNESS, HISTORY, LIFESTYLE, MOVIES, MUSIC, NEWS, BUSINESS, REALITY, RELIGION, SCIENCE &amp; NATURE, SHOPPING, SPORTS, WEATHER, to be announced, space, wedding, skills competition, school info, 3D, action sports, architecture, Australian football, behind-the-scenes, best of, Bollywood, celebrity sports, classic sports, construction, countdown, darts, dating, decorating, emo, engineering, fireworks, Gaelic football, goth, green, hurling, red carpet, preview, poker, photography, mockumentary, military, makeover, lumberjack competition, literature, legal, landscaping, jewelry, jet skiing, imax, internet, reality competition

## PgmRatingTypeDataType
A string with a value in the following list:
* MPAA, US TV, CTV, OFRB, FCTV, Age Rating, Family Rating, TV Star Rating, RCQ, Austria TV, Belgium TV, Denmark TV, Finland TV, France TV, Germany TV, Ireland TV, Italy TV, Netherlands TV, Norway TV, Qatar TV, Spain TV, Sweden TV, Switzerland TV, United Kingdom TV, Luxembourg TV, Poland TV, Belgacom Ratings, Brazil TV, Portugal TV, Russia TV, Argentina: INCAA, Mexico TV, Panama TV, Spain: MCU, France: CNC, Germany: FSK, United Kingdom: BBFC, Ireland: IFCO, NL: kijkwijzer, Italy: MiBAC, Denmark: Medieraadet, Norway Medietilsynet, Sweden: Medierad, Finland: Meku, Austria: JMK, Poland, Switzerland: KJ, Portugal: CCE, Russia: MKRF, Chile: CCC, Mexico: RTC, Brazil: DEJUS, Panama, El Salvador 

## PgmRatingDataType
A string with a value in the following list:
* +13, +16, +18, ¡A, 0, 0+, 1, 10, 11, 12, 12+, 12A, 13, 13+, 14, 14+, 14A, 15, 15A, 16, 16+, 17, 18, 18+, 18A, 2, 21, 3, 4, 5, 6, 6+, 7, 8, 8+, 9, A, AA, AL, All, ATP, B, B-15, b.o., Barn., C, C8, D, E, FSK: 0, FSK: 12, FSK: 16, FSK: 18, FSK: 3, FSK: 6, FSK: 8, G, K12, K16, K18, K7, L, M/12, M/16, M/18, M/4, M/6, NC-17, None, NR, PG, PG-13, R, R18, S, T, TE, TE7+, Tous, TP, TV-14, TV-14@D, TV-14@DL, TV-14@DLS, TV-14@DLSV, TV-14@DLV, TV-14@DS, TV-14@DSV, TV-14@DV, TV-14@L, TV-14@LS, TV-14@LSV, TV-14@LV, TV-14@S, TV-14@SV, TV-14@V, TV-G, TV-MA, TV-MA@L, TV-MA@LS, TV-MA@LSV, TV-MA@LV, TV-MA@S, TV-MA@SV, TV-MA@V, TV-PG, TV-PG@D, TV-PG@DL, TV-PG@DLS, TV-PG@DLSV, TV-PG@DLV, TV-PG@DS, TV-PG@DSV, TV-PG@DV, TV-PG@L, TV-PG@LS, TV-PG@LSV, TV-PG@LV, TV-PG@S, TV-PG@SV, TV-PG@V, TV-Y, TV-Y7, TV-Y7@FV, U, X

## EventRatingTypeDataType
A string with a value in the following list:
* MPAA, US TV, CTV, OFRB, FCTV, Age Rating, Family Rating, TV Star Rating, RCQ, Austria TV, Belgium TV, Denmark TV, Finland TV, France TV, Germany TV, Ireland TV, Italy TV, Netherlands TV, Norway TV, Qatar TV, Spain TV, Sweden TV, Switzerland TV, United Kingdom TV, Luxembourg TV, Poland TV, Belgacom Ratings, Brazil TV, Portugal TV, Russia TV, Argentina: INCAA, Mexico TV, Panama TV, Spain: MCU, France: CNC, Germany: FSK, United Kingdom: BBFC, Ireland: IFCO, NL: kijkwijzer, Italy: MiBAC, Denmark: Medieraadet, Norway Medietilsynet, Sweden: Medierad, Finland: Meku, Austria: JMK, Poland, Switzerland: KJ, Portugal: CCE, Russia: MKRF, Chile: CCC, Mexico: RTC, Brazil: DEJUS, Panama, El Salvador 

## EventRatingDataType
A string with a value in the following list:
* +13, +16, +18, ¡A, 0, 0+, 1, 10, 11, 12, 12+, 12A, 13, 13+, 14, 14+, 14A, 15, 15A, 16, 16+, 17, 18, 18+, 18A, 2, 21, 3, 4, 5, 6, 6+, 7, 8, 8+, 9, A, AA, AL, All, ATP, B, B-15, b.o., Barn., C, C8, D, E, FSK: 0, FSK: 12, FSK: 16, FSK: 18, FSK: 3, FSK: 6, FSK: 8, G, K12, K16, K18, K7, L, M/12, M/16, M/18, M/4, M/6, NC-17, None, NR, PG, PG-13, R, R18, S, T, TE, TE7+, Tous, TP, TV-14, TV-14@D, TV-14@DL, TV-14@DLS, TV-14@DLSV, TV-14@DLV, TV-14@DS, TV-14@DSV, TV-14@DV, TV-14@L, TV-14@LS, TV-14@LSV, TV-14@LV, TV-14@S, TV-14@SV, TV-14@V, TV-G, TV-MA, TV-MA@L, TV-MA@LS, TV-MA@LSV, TV-MA@LV, TV-MA@S, TV-MA@SV, TV-MA@V, TV-PG, TV-PG@D, TV-PG@DL, TV-PG@DLS, TV-PG@DLSV, TV-PG@DLV, TV-PG@DS, TV-PG@DSV, TV-PG@DV, TV-PG@L, TV-PG@LS, TV-PG@LSV, TV-PG@LV, TV-PG@S, TV-PG@SV, TV-PG@V, TV-Y, TV-Y7, TV-Y7@FV, U, X


## StarRatingDataType
A string with a value in the following list:
* None, 1, 2, 3, 4

## AspectRatioDataType
A string with a value in the following list:
* 4:3 Letterbox, 16:9 Fullscreen, 4:3 Fullscreen, 4:3 Unknown, 16:9 Letterbox, 16:9 Unknown, Letterbox, Unknown, Pillarbox

## ThreeDFormatDataType
A string with a value in the following list:
* None, Sequential, 3D Level Unknown, Side-by-Side

## SourceRegionDataType
A string with a value in the following list:
* North America, Europe

## ImageTypeDataType
A string with a value in the following list:
* Head Shot: Key, Group, Gallery: Key, Gallery: Supporting, Program: Key, Box Art, Production: Key, Program Logo, Team Logo, League Logo, Key Art, Station Logo, Head Shot: Supporting, Program: Supporting, Production: Supporting, Celebrity, Trailer, Provider Logo, Album Cover Front, Album Cover Back, DVD Box Art, Video Box Art, Poster Art, DVD Set, Showcard, Vertical Showcard (3:4)

## ImageFileFormatDataType
A string with a value in the following list:
* jpg, jpeg, png