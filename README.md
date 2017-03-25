# pypod

This project is a simple, commandline podcast catcher that accomplishes the following goals:

1) Completely configurable via a simple JSON file.
2) Minimum requirements: feedparser and requests
3) Completely command line.
4) Automatically creates folders for each podcast.
5) Prepends each podcast entry with its date so you always know what the latest entry was.
6) Limit downloaded podcast files, per podcast (auto cleanup of old podcasts)

## Directions

1) Configure requirements:

    pip3 install -r requirements.txt

2) Configure cron entry (if you're using *nix):

    0 *  *   *   *     /opt/pypod/pypod

3) Edit config.json:

These settings should be pretty straight-forward, but here's an example to get you started:

    {
        "root_folder":"/opt/pypod/Podcasts/",
        "keep_per_podcast":10,
        "download_threads":10,
        "podcasts":[
            {
                "folder":"The Jason Stapleton Program",
                "url":"https://audioboom.com/channels/4667410.rss"
            },
            {
                "folder":"The Fifth Column",
                "url":"http://fifthcolumn.podbean.com/feed/"
            }
        ]
    }

The `root_folder` should already exist.  Each `folder` will be created as necessary.

The `keep_per_podcast` is the number of episodes to keep for each podcast.  In the above example, if more than 10 podcasts exist in the folder, the last ten will be saved and the rest deleted.

The `download_threads` option dictates how many different podcasts will be downloaded simultaneously.  This is threaded per podcast and not per episode due to many podcast feeds throttling multiple episode downloads of the same podcast. 

## Caveats

If your feed contains any unicode and you are running this script in Windows, please make sure to run the following console command prior to running pypod, or you will get an exception due to the unicode characters:

    chcp 65001 
