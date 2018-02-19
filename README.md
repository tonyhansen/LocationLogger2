# LocationLogger2

## PHP App to gather, edit GPS coordinates and meta-data on houses/apartments

We have special needs that Google maps does not satisfy. This project is about logging the data points and associated meta-data. We have already had this project done as an app (which we will use later) but right now need the simplicity of a pure PHP/Javascript/MySQL page (not an app). We will use a blue-tooth, smartphone connected, GPS device to get accurate positions (approximate data from a phone GPS is enough to test).

One screen is needed with _“Get My Coordinates”_ and _“Save”_ buttons. Pressing _Save_ creates a record in the location table (you do not need to create screens to administer the streets, blocks or territories tables). This app thus logs a series of coordinates by simply walking along and pressing the _Get_ and _Save_ buttons at the front gate of each dwelling (with no other meta-data specified).

However for entry of additional meta-data, the app would also offer (below the _Save_ button):

* A popup, selection persistent list to choose coordinate type: Dwelling (1), Street vertex (2), Block outline vertex (3)
* House or Apartment Number (with adjacent keypad that feeds only to it, it zeros after save unless incrementor set)
* House number incrementor (remains static, can be negative, if specified each Save adds this to the house number)
* A note field (zeros after save)
* Territory Number picker (persistent)
* Block Number picker (persistent)
* Street/Avenue Picker (persistent)

_“Get My Coordinates”_ checks if the current location is within 3 meters of a known one.
If so it fills the meta fields with its data (and overwrites the existing record on save).

CREATE TABLE `location` (
  `location_id` int(11) NOT NULL,
  `location_type` tinyint(4) NOT NULL,
  `geopoint` point NOT NULL,
  `street_id` int(11) DEFAULT NULL,
  `block_id` int(11) DEFAULT NULL,
  `territory_id` int(11) DEFAULT NULL,
  `number` varchar(99) COLLATE utf8_unicode_ci DEFAULT NULL,
  `notes` mediumtext COLLATE utf8_unicode_ci,
  `birthdate` date NOT NULL,
  `moddate` date NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_unicode_ci;

CREATE TABLE `blocks` (
  `block_id` int(11) NOT NULL AUTO_INCREMENT,
  `name` varchar(99) COLLATE utf8_unicode_ci NOT NULL,
  `birthdate` date NOT NULL,
  `moddate` date NOT NULL,
  PRIMARY KEY (`block_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_unicode_ci;

CREATE TABLE `streets` (
  `street_id` int(11) NOT NULL AUTO_INCREMENT,
  `name` varchar(99) COLLATE utf8_unicode_ci NOT NULL,
  `birthdate` date NOT NULL,
  `moddate` date NOT NULL,
  PRIMARY KEY (`street_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_unicode_ci;

CREATE TABLE `territories` (
  `territory_id` int(11) NOT NULL AUTO_INCREMENT,
  `name` varchar(99) COLLATE utf8_unicode_ci NOT NULL,
  `birthdate` date NOT NULL,
  `moddate` date NOT NULL,
  PRIMARY KEY (`territory_id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_unicode_ci;

