# GO Monitoring, and sending data to TimeSeries (opentsdb at this time)

The package sends a go application internal monitoring metrics to tsdb.

It is also expandable and other data can be added.

## Dependencies
github.com/abkhan/opentsdb-httpclient

github.com/abkhan/config

## Usage

Get a function from gomonts to add metrics to tsdb, by supplying it with;
 - the name of the app
 - the version of the app
 - the config for tsdb

 ```
 addfunc := gomonts.GoMoInit(app-name, "0.0.2", c.Tsdb)
 ```

 The GoMoInit sends go app metrics to tsdb every minute.

 To add additional metrics, use the addfunc;

 ```
 tags := []tsdb.Tag{{Key: "failed", Value: fmt.Sprintf("%d", errorc)}}
	addfunc("ping", float64(int64(avgDur)/1000000), tags)
```

This will create a metric name `app-name.ping`, where app-name is the name used in GoMoInit function.

### TSDB Config

```
tsdb:
  host: 192.168.0.139
  port: 4242
  defaultBuffer: 1
  defaultInterval: 1
  metric: conn
  http:
    dialTimeout: 3s
    tlsHandShakeTimeout: 3s 
    maxIdleConnsPerHost: 20
    maxIdleConns: 20
    idleConnTimeout: 2m   
    clientTimeout: 5s  
```

### Example app that uses this package
githut.com/abkhan/conntest

## Dev Status
Work in progress, bugs expected, enhancements needed.