---
title: Combining event streams
keywords: vega
sidebar: vega_sidebar
permalink: vega-combining-event-streams.html
folder: vega
---
Often you will want to filter event _streams_ (e.g. to throttle them so that you only get a signal every 5 seconds or so), or combine them.

A _single_ event stream is defined as described above.

<img src="{{ site.baseurl }}/assets/vega-event-singlestream.png" width="50%" />

Streams can be _filtered_ so that not all events trigger a signal. In the picture below, the top stream is the original and the bottom stream is the one that gets through to the signal. For example, a click event is only allowed to get into the target stream if the click is in a place that is at least 300 pixels from the left of the screen, and the price in the dtaset is smaller than 500.

<img src="{{ site.baseurl }}/assets/vega-event-filteredstreams.png" width="50%" />

You can also filter events in a stream by whether or not they are between two other events. In this example, only mousemoves that are between a mousedown and mouseup are passed on. This is basically a drag.

<img src="{{ site.baseurl }}/assets/vega-event-between.png" width="50%" />

You can _merge_ different streams into one.

<img src="{{ site.baseurl }}/assets/vega-event-mergestreams.png" width="50%" />

And finally you can also _throttle_ event streams so that only a certain number of events get through in a given period of time.

<img src="{{ site.baseurl }}/assets/vega-event-throttled.png" width="50%" />
