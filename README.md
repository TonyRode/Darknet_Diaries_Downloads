# Darknet_Diaries_Downloads
Bash onliner to download all darknet diaries episodes

```
#!/bin/bash
darknet_diaries_feed_parsed=$(curl -s https://feeds.megaphone.fm/darknetdiaries | grep -E '<title>|enclosure'); while read -r title; do read -r enclosure; export title; export enclosure; name=$(echo "$title" | sed 's/  / /g' | sed 's/[#!,()]//g' | sed -E 's/<.{5,6}>//g' | sed 's/[: ]/_/g')".mp3"; url=$(echo "$enclosure" | grep -oE "h.*p3"); if [[ "${name:0:1}" == "P" ]]; then name="Ep_65_2__$name"; fi; if [[ "${name:0:2}" != "Ep" ]]; then name="Ep_$name"; fi; name="Darknet_Diaries_$name"; echo "Downloading ... $name .. $url"; curl -Lo "$name" "$url" ; done <<< "$(echo "$darknet_diaries_feed_parsed" | sed '1,2d')";
```

You can easily adapt it to name it the way you like using the "name" parameter, make a cronjob and download only the last ones if the file already exists and so on.

Enjoy !


ps: You can also use something like Podcast Addict (thanks das for the recommendation !), which is a very handy app.
