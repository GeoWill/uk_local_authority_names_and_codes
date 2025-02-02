---
name: uk_la_future
title: UK Local Authorities (including future)
description: "A dataset that includes current and previous local authorities, as well\
  \ as some planned but not in force yet\n"
version: latest
keywords:
- UK Local data
- United Kingdom
licenses:
- name: CC-BY-4.0
  path: https://creativecommons.org/licenses/by/4.0/
  title: Creative Commons Attribution 4.0 International License
contributors:
- title: mySociety
  path: https://mysociety.org
  role: author
custom:
  build: uk_local_authority_names_and_codes.build:create_future_only
  dataset_order: 2
  tests:
  - test_basic_requirements
  - test_time
  - test_values
  download_options:
    gate: default
    survey: default
    header_text: default
  composite:
    xlsx:
      include: all
      exclude: none
      render: true
    sqlite:
      include: all
      exclude: none
      render: true
    json:
      include: all
      exclude: none
      render: true
  change_log:
    0.1.0: Initial commit of new data
    0.1.1: Added dataset order to config
    1.0.0: Increment to fixed version
    1.0.1: "description changed from 'A dataset that include current and previous\
      \ local authorities, as well as some planned but not in force yet\n' to 'A dataset\
      \ that includes current and previous local authorities, as well as some planned\
      \ but not in force yet\n'"
    1.0.2: keywords changed from 'None' to '['UK Local data', 'UK']'
    1.0.3: keywords changed from '['UK Local data', 'UK']' to '['UK Local data', 'United
      Kingdom']'
    1.0.4: 'Minor change in data for resource(s): uk_local_authorities_future'
    1.0.5: 'Minor change in data for resource(s): uk_local_authorities_future'
    1.0.6: 'Minor change in data for resource(s): uk_local_authorities_future'
resources:
- title: UK Local Authorities (past/current/future)
  description: Table of information about local authorities, and mapping between different
    ID schemes. Includes current, some past, and some future authorities.
  custom:
    row_count: 466
  path: uk_local_authorities_future.csv
  name: uk_local_authorities_future
  profile: tabular-data-resource
  scheme: file
  format: csv
  hashing: md5
  encoding: utf-8
  schema:
    fields:
    - name: local-authority-code
      type: string
      description: Fixed ID for council, not linked to boundary changes. Based on
        old local authorities register.
      constraints:
        unique: true
      example: ABC
    - name: official-name
      type: string
      description: Official long name for council (may not *always* be legal name)
      constraints:
        unique: true
      example: Armagh City, Banbridge and Craigavon Borough Council
    - name: nice-name
      type: string
      description: A shorter name for the council.
      constraints:
        unique: false
      example: Armagh City, Banbridge and Craigavon
    - name: gss-code
      type: string
      description: The code for the statistical geography of the boundaries of the
        authority
      constraints:
        unique: false
      example: N09000002
    - name: start-date
      type: string
      description: The date the authority came into existance (YYYY-MM-DD). Can be
        blank.
      constraints:
        unique: false
      example: '2015-04-01'
    - name: end-date
      type: string
      description: The date the authority was abolished (YYYY-MM-DD). Can be blank.
      constraints:
        unique: false
      example: '2023-04-01'
    - name: replaced-by
      type: string
      description: If the council was abolished a comma seperated list of successor
        bodies. Comma seperated when there are multiple (rare - when a county council
        area is divided into two unitaries).
      constraints:
        unique: false
      example: CBD
    - name: nation
      type: string
      description: Nation of the UK (England, Scotland, Wales, Northern Ireland)
      constraints:
        unique: false
        enum:
        - Northern Ireland
        - Scotland
        - England
        - Wales
      example: Northern Ireland
    - name: region
      type: string
      description: English region, but using the nation for non-English authorities.
      constraints:
        unique: false
      example: Northern Ireland
    - name: local-authority-type
      type: string
      description: The short-code for type of local authority.
      constraints:
        unique: false
        enum:
        - NID
        - SCO
        - NMD
        - WPA
        - UA
        - LBO
        - MD
        - CTY
        - COMB
        - SRA
        - CC
      example: NID
    - name: local-authority-type-name
      type: string
      description: The name of the type of local authority.
      constraints:
        unique: false
        enum:
        - NI district
        - Scottish unitary authority
        - Non-metropolitan district
        - Welsh unitary authority
        - Unitary authority
        - London borough
        - Metropolitan district
        - County
        - Combined authority
        - Strategic Regional Authority
        - City corporation
      example: NI district
    - name: county-la
      type: string
      description: If this council overlaps with a county council, the local-authority-code
        of this council. Can be none.
      constraints:
        unique: false
      example: WSX
    - name: combined-authority
      type: string
      description: If the council overlaps with a combined authority, the local-authority-code
        of this council. Can be done.
      constraints:
        unique: false
      example: WECA
    - name: alt-names
      type: string
      description: Comma seperated list of alternative names for a local authority.
      constraints:
        unique: true
      example: Armagh City, Banbridge and Craigavon,armagh city, banbridge and craigavon,armagh,
        banbridge and craigavon
    - name: former-gss-codes
      type: string
      description: A list of any gss codes for an area that apply to the former boundaries
        of a local authority.
      constraints:
        unique: false
      example: S12000009
    - name: notes
      type: string
      description: Any notes on columns or values that require special interpretation.
      constraints:
        unique: false
      example: gss code is for London region - when working from code point open use
        E18000007 and the NHS_HA_code column
    - name: current-authority
      type: boolean
      description: a boolean saying if the authority is currently a legal authority
        (not a past or future authority)
      constraints:
        unique: false
        enum:
        - true
        - false
      example: 'True'
    - name: BS-6879
      type: string
      description: A 3-4 letter code for the authority. Substancially the same as
        local-authority-code, but local-authority-code is now assigned seperately
        and there may be drift.
      constraints:
        unique: false
      example: ABC
    - name: ecode
      type: string
      description: A code for local authorities used in financial documents.
      constraints:
        unique: false
      example: E3831
    - name: even-older-register-and-code
      type: string
      description: A combination of register and code used in the former official
        registers.
      constraints:
        unique: false
      example: local-authority-wls:AGY
    - name: gov-uk-slug
      type: string
      description: A url slug for an authority used by gov.uk
      constraints:
        unique: false
      example: armagh-banbridge-craigavon
    - name: area
      type: number
      description: The area of the boundaries of a local authority, in km squared.
      constraints:
        unique: false
      example: 1338.0
    - name: pop-2020
      type: number
      description: The estimated number of people living in the local authority in
        2020.
      constraints:
        unique: false
      example: 217232.0
    - name: x
      type: number
      description: X coordinate for the center of the local authority.
      constraints:
        unique: false
      example: 110637.83710267964
    - name: y
      type: number
      description: Y coordinate for the center of the local authority.
      constraints:
        unique: false
      example: 506234.41480476985
    - name: long
      type: number
      description: Longitude of the center of the local authority
      constraints:
        unique: false
      example: 54.36919159394883
    - name: lat
      type: number
      description: Latitude of the center of the local authority
      constraints:
        unique: false
      example: -6.456724092266463
    - name: powers
      type: string
      description: A grouping of local authority type based on the actual powers of
        an area (merges several effective 'unitary' categories)
      constraints:
        unique: false
        enum:
        - ni district
        - unitary
        - lower tier
        - upper tier
        - combined
      example: ni district
    - name: lower-or-unitary
      type: boolean
      description: Boolean stating if the council is a district (lower tier) or unitary
        council
      constraints:
        unique: false
        enum:
        - true
        - false
      example: 'True'
    - name: mapit-area-code
      type: string
      description: Where avaliable, the kind of geography this authority is in mapit.
      constraints:
        unique: false
      example: DIS
    - name: ofcom
      type: string
      description: Variant on snac authority code used in coding survey responses
      constraints:
        unique: false
      example: 95-OQN
    - name: old-ons-la-code
      type: string
      description: Old ONS code for local authorities.
      constraints:
        unique: false
      example: 45UB
    - name: old-register-and-code
      type: string
      description: A lookup to the paired register and code on the former register
        project.
      constraints:
        unique: false
      example: local-authority-nir:ABC
    - name: open-council-data-id
      type: number
      description: The id used for the council on opencouncildata.co.uk/
      constraints:
        unique: false
      example: 1002.0
    - name: os-file
      type: string
      description: Form of name used in some ordnance survey datasets.
      constraints:
        unique: false
      example: ABERDEENSHIRE
    - name: os
      type: number
      description: Numeric ID assigned by ordnance survey
      constraints:
        unique: false
      example: 7000000000030110.0
    - name: snac
      type: string
      description: Old ONS Standard Names and Codes code
      constraints:
        unique: false
      example: 00QB
    - name: wdtk-id
      type: number
      description: ID of authority in WhatDoTheyKnow
      constraints:
        unique: false
      example: 54906.0
  _sheet_order: 1
  hash: edeb4cf1869d74685086f2767a898c08
  download_id: uk-la-future-uk-local-authorities-future
full_version: 1.0.6
permalink: /datasets/uk_la_future/latest
---
