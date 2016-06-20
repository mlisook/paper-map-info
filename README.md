# paper-map-info

An element that displays a <paper-material> backed infowindow-like card on a <google-map> element at the position of a map marker.

## WHY!?

In its current implementation (as of June 2016) the native infowindow does not support event handlers, so interactive infowindows are out.  For example:

    <google-map-marker ...>
      <paper-button on-tap="makeReservation">Reserve</paper-button>
      ...
    </google-map-marker>
This will not work because the on-tap binding is lost when the infowindow is built. There is an issue open ([#288](https://github.com/GoogleWebComponents/google-map/issues/288)), but as of now it is not resolved.

If you don't need event handlers in the infowindow _use the native infowindow_.  If you do, this element may help you.

## Normal Infowindow Functionality Supported

Normal Google Map infowindow behavior is supported, including moving the window as the user pans the map, changes zoom, or drags the marker. The behavior where the map pans automatically to allow the infowindow to be displayed when the clicked marker was too close to an edge is also supported. In addition, since dynamic content is allowed, if the size of the content changes the position of the window will adjust accordingly.

## Sample Usage

    <google-map latitude="40.7555" longitude="-73.985" on-google-map-ready="mapReady" fit-to-markers>
      <template is="dom-repeat" items="[[salons]]" as="s">
        <google-map-marker click-events latitude="[[s.lat]]" longitude="[[s.lng]]" on-google-map-marker-click="markerClick">
        </google-map-marker>
      </template>
      <paper-map-info id="myinfocard" fade-in>
        <div class="layout vertical">
          <div style="width:100%; background-color: blue; font-weight: bold; color: white; padding: 5px;">[[selectedSalon.name]]</div>
          <div class="layout vertical" style="border: 2px solid blue; padding: 5px;">
            <paper-button raised on-tap="booking">Book an Appointment</paper-button>
          </div>
        </div>
      </paper-map-info>
    </google-map>

    markerClick: function(e) {
      this.selectedSalon = e.model.get('s');
      this.$.myinfocard.showInfoWindow(e.srcElement.marker);
    }

The element is meant to be fully composable so you can have anything inside, even neon-animated-pages, if you want.

## Styling

You can customize the paper-material background using the `--paper-map-info-mixin`.  You can customize the style of the beak (pointer from the card to the pin) with `--paper-map-info-beak-mixin`. Or even replace the default beak entirely with:

    <div class="paper-map-info-beak">
      ... your image or svg here ...
    <div>
inside the content of the paper-map-info.

## Install in Your Project

Install with bower:

`bower install --save paper-map-info`

## Dependencies

Element dependencies are managed via [Bower](http://bower.io/). You can
install that via:

    npm install -g bower

Then, go ahead and download the element's dependencies:

    bower install


## Viewing the Element Pages and Demo

Use [Polyserve](https://github.com/PolymerLabs/polyserve) to serve up the element documentation and demo. You can install it via:

    npm install -g polyserve

And you can run it via:

    polyserve

Once running, you can preview your element at
`http://localhost:8080/components/paper-map-info/`, where `paper-map-info` is the name of the directory containing it.

## Issues and Contributions

Please file issues on the github page. Contributions via pull request are certainly welcome.
