# Pynoptes

Pynoptes is a better name than this script deserves. It's a python script that reads the Zooniverse AWS Kinesis stream and yarks it onto your command line.

Use it like this:

`python read_stream.py zooniverse-production --worker_time 10 --echo`

The first argument should be the stream name. In this case, `zooniverse-production`.

`--region` does what you think, but the default is fine.

`--worker_time` is going to set how long the script runs before it sums up and quits.

`--sleep_interval` sets the amount of time between requests. Increase if you're getting a ton of rate limiting errors.

`--echo` is gonna just yark the stream all over. Without `--echo`, the only stream data that will be printed is the annotation, if applicable.

This script will start a new thread for each shard, but Zooniverse just runs the one.
        
This is basically forked from [Amazon's own example](https://github.com/awslabs/kinesis-poster-worker).
