## quintana

A simple wrapper to lazily create Folsom metrics.

![quintana](http://i.imgur.com/kyEAS9B.gif)

### Metrics types
(source: [boundary/folsom](https://github.com/boundary/folsom#metrics-api))

#### Counters
Counter metrics provide increment and decrement capabilities for a single scalar value.

#### Gauges
Gauges are point-in-time single value metrics.

#### Histograms (and Timers)
Histograms are collections of values that have statistical analysis done to them, such as mean, min, max, kurtosis and percentile. They can be used like "timers" as well with the timed update functions.

##### Histogram sample types
Each histogram draws its values from a reservoir of readings. You can select a sample type for a histogram by passing the name of the sample type as an atom when you create a new histogram. Some sample types have further arguments. The purpose of a sample type is to control the size and charecteristics of the reservoir of readings the histogram performs analysis upon.

Folsom currently provides the following sample types:

###### uniform
This is a random uniform sample over the stream of readings. This is the default sample type, bounded in size to 1028 readings. When size readings have been taken, new readings replace older readings in the reservoir at random.

###### exdec
This is a sample that exponentially decays less significant readings over time so as to give greater significance to newer readings.

###### slide
This is a sliding window in time over a stream of readings. The default window size is 60 seconds. Every reading that occurs in a sliding sixty second window is stored, with older readings being discarded. If you have a lot of readings per minute the reservoir may get pretty big and so it will take more time to calculate statistics. You can set the window size by providing a number of seconds.

###### slide_uniform
This is a sliding window in time over a stream of readings with a random uniform sample per second, to bound the size of the total number of readings. The maximum size of the reservoir will be  window size * sample size. Default is a window of 60 seconds and a sample size of 1028.

#### Histories
Histories are a collection of past events, such as errors or log messages.

#### Meters
Meters are increment only counters with mean rates and exponentially weighted moving averages applied to them, similar to a unix load average.

#### Spiral meter
A spiral is a type of meter that has a one minute sliding window count. The meter tracks an increment only counter and a total for the last minute. This is a sliding count with older readings dropping off per second.

#### Meter Reader
Meter readers are like a meter except that the values passed to it are monotonically increasing, e.g., reading from a water or gas meter, CPU jiffies, or I/O operation count.
