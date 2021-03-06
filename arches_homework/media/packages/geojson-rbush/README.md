# GeoJSON RBush

[![Build Status](https://travis-ci.org/DenisCarriere/geojson-rbush.svg?branch=master)](https://travis-ci.org/DenisCarriere/geojson-rbush)
[![npm version](https://badge.fury.io/js/geojson-rbush.svg)](https://badge.fury.io/js/geojson-rbush)
[![MIT licensed](https://img.shields.io/badge/license-MIT-blue.svg)](https://raw.githubusercontent.com/DenisCarriere/geojson-rbush/master/LICENSE)

GeoJSON implementation of [RBush](https://github.com/mourner/rbush) — a high-performance JavaScript R-tree-based 2D spatial index for points and rectangles.

## Install

**npm**

```bash
$ npm install --save geojson-rbush
```

## API

<!-- Generated by documentation.js. Update this documentation by updating the source code. -->

#### Table of Contents

-   [rbush](#rbush)
-   [insert](#insert)
-   [load](#load)
-   [remove](#remove)
-   [clear](#clear)
-   [search](#search)
-   [collides](#collides)
-   [all](#all)
-   [toJSON](#tojson)
-   [fromJSON](#fromjson)

### rbush

GeoJSON implementation of [RBush](https://github.com/mourner/rbush#rbush) spatial index.

**Parameters**

-   `maxEntries` **[number](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number)** defines the maximum number of entries in a tree node. 9 (used by default) is a
    reasonable choice for most applications. Higher value means faster insertion and slower search, and vice versa. (optional, default `9`)

**Examples**

```javascript
var rbush = require('geojson-rbush')
var tree = rbush()
```

Returns **RBush** GeoJSON RBush

### insert

[insert](https://github.com/mourner/rbush#data-format)

**Parameters**

-   `feature` **Feature&lt;any>** insert single GeoJSON Feature

**Examples**

```javascript
var polygon = {
  "type": "Feature",
  "properties": {},
  "geometry": {
    "type": "Polygon",
    "coordinates": [[[-78, 41], [-67, 41], [-67, 48], [-78, 48], [-78, 41]]]
  }
}
tree.insert(polygon)
```

Returns **RBush** GeoJSON RBush

### load

[load](https://github.com/mourner/rbush#bulk-inserting-data)

**Parameters**

-   `features` **([Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)&lt;BBox> | FeatureCollection&lt;any>)** load entire GeoJSON FeatureCollection

**Examples**

```javascript
var polygons = {
  "type": "FeatureCollection",
  "features": [
    {
      "type": "Feature",
      "properties": {},
      "geometry": {
        "type": "Polygon",
        "coordinates": [[[-78, 41], [-67, 41], [-67, 48], [-78, 48], [-78, 41]]]
      }
    },
    {
      "type": "Feature",
      "properties": {},
      "geometry": {
        "type": "Polygon",
        "coordinates": [[[-93, 32], [-83, 32], [-83, 39], [-93, 39], [-93, 32]]]
      }
    }
  ]
}
tree.load(polygons)
```

Returns **RBush** GeoJSON RBush

### remove

[remove](https://github.com/mourner/rbush#removing-data)

**Parameters**

-   `feature` **(BBox | Feature&lt;any>)** remove single GeoJSON Feature

**Examples**

```javascript
var polygon = {
  "type": "Feature",
  "properties": {},
  "geometry": {
    "type": "Polygon",
    "coordinates": [[[-78, 41], [-67, 41], [-67, 48], [-78, 48], [-78, 41]]]
  }
}
tree.remove(polygon)
```

Returns **RBush** GeoJSON RBush

### clear

[clear](https://github.com/mourner/rbush#removing-data)

**Examples**

```javascript
tree.clear()
```

Returns **RBush** GeoJSON Rbush

### search

[search](https://github.com/mourner/rbush#search)

**Parameters**

-   `geojson` **(BBox | FeatureCollection | Feature&lt;any>)** search with GeoJSON

**Examples**

```javascript
var polygon = {
  "type": "Feature",
  "properties": {},
  "geometry": {
    "type": "Polygon",
    "coordinates": [[[-78, 41], [-67, 41], [-67, 48], [-78, 48], [-78, 41]]]
  }
}
tree.search(polygon)
```

Returns **FeatureCollection&lt;any>** all features that intersects with the given GeoJSON.

### collides

[collides](https://github.com/mourner/rbush#collisions)

**Parameters**

-   `geojson` **(BBox | FeatureCollection | Feature&lt;any>)** collides with GeoJSON

**Examples**

```javascript
var polygon = {
  "type": "Feature",
  "properties": {},
  "geometry": {
    "type": "Polygon",
    "coordinates": [[[-78, 41], [-67, 41], [-67, 48], [-78, 48], [-78, 41]]]
  }
}
tree.collides(polygon)
```

Returns **[boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean)** true if there are any items intersecting the given GeoJSON, otherwise false.

### all

[all](https://github.com/mourner/rbush#search)

**Examples**

```javascript
tree.all()
//=FeatureCollection
```

Returns **FeatureCollection&lt;any>** all the features in RBush

### toJSON

[toJSON](https://github.com/mourner/rbush#export-and-import)

**Examples**

```javascript
var exported = tree.toJSON()
//=JSON object
```

Returns **any** export data as JSON object

### fromJSON

[fromJSON](https://github.com/mourner/rbush#export-and-import)

**Parameters**

-   `json` **any** import previously exported data

**Examples**

```javascript
var exported = {
  "children": [
    {
      "type": "Feature",
      "geometry": {
        "type": "Point",
        "coordinates": [110, 50]
      },
      "properties": {},
      "bbox": [110, 50, 110, 50]
    }
  ],
  "height": 1,
  "leaf": true,
  "minX": 110,
  "minY": 50,
  "maxX": 110,
  "maxY": 50
}
tree.fromJSON(exported)
```

Returns **RBush** GeoJSON RBush
