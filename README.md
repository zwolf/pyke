# Pyke

Pyke is a few python scripts that read the Zooniverse AWS Kinesis stream and yark it onto your command line. It has a few different flavors.

## KCL

The first is the delicious AWS KCL implementation. This flavor depends on the KCL Java libraries, so install those first:

* `git clone git@github.com:awslabs/amazon-kinesis-client-python.git`
* `python setup.py download_jars`
* `python setup.py install`

Make any necessary changes to `zooniverse.properties`. To run it, the command is gonna look like this:

`$(python ./kcl_helper.py --print_command --properties path/to/zooniverse.properties --java /path/to/java)`

This will execute the big ol' java command that the helper creates. Ensure that java is installed and correct its path above, along with the one to your properties file. You'll get a bunch of noise along with the Zooniverse data up on your console. We'll make this more useful soon.

You're going to want to make sure that you use the appropriate path to your python executable on top of these scripts. Also, if zoostream.py can still not be found, try adding the path to pyke to your $PATH.

Based on [this](https://github.com/awslabs/amazon-kinesis-client-python).

## Boto

You can also use the boto-based, non-KCL stream reader:

`python read_stream.py zooniverse-production --worker_time 10 --echo`

The first argument should be the stream name. In this case, `zooniverse-production`.

`--region` does what you think, but the default is fine.

`--worker_time` is going to set how long the script runs before it sums up and quits.

`--sleep_interval` sets the amount of time between requests. Increase if you're getting a ton of rate limiting errors.

`--echo` is gonna just yark the stream all over. Without `--echo`, the only stream data that will be printed is the annotation, if applicable.

This script will start a new thread for each shard, but Zooniverse just runs the one.

This is also based on [Amazon's own example](https://github.com/awslabs/kinesis-poster-worker).
