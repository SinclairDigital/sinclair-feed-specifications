# Sinclair External Linear Feed

### Overview

This guide includes detailed information on the Sinclair External Linear Feed Specification, which can be used to build a content feed of linear video content. This schema conforms to the TIVO/Rovi XML Schema for program scheduling ([XSD](rovi-docs-and-xml/RoviExternalListings.xsd) [Data Types](rovi-docs-and-xml/RoviExternalListingsDataTypes.xsd))

**Sections:**
* [Linear Feed Schema](#linear-feed-schema)

**Content types:**
* [Rovi Listings](#rovi-listings)
  * [Programs](#programs)
    * [Station](#station)
* [EventRatingTypeDef](#eventratingtypedef)
  * [EventRating](#eventrating)
    * [RatingReasons](#ratingreasons)
      * [RatingReason](#ratingreason)
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
    * [EventRatingTypeDef](#eventratingtypedef)
    * [MiscAttributes](#miscattributes)
  *  * [Attribute](#attribute)
* [ProgramTypeDef](#)
  * [AlternateTitles](#alternatetitles)
    * [Title](#title)
      * [AltTitleType](#alttitletype)
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
These are the properties for the root object of your feed. It contains basic information such as your company's name, when the feed was last updated, and other objects that will describe all your content such as TV Shows, Movies, etc.

| Field | Type | Required | Description |
| ----- | ---- | -------- | ----------- |
|  |  |  | 
|  |  |  | 
|  |  |  | 
|  |  |  | 
|  |  |  | 



---

## Rovi Listings

## Program
  

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
