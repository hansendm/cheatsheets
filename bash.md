# If you want them to be started # the background and run sequentially, you would do something like this:

{ sleep 2; sleep 3; } &

# If you want sleep 3 to run only if sleep 2 succeeds, then:

sleep 2 && sleep 3 &

# If, on the other hand, you would like them to run in parallel in the background, you can instead do this:

sleep 2 & sleep 3 &

# And the two techniques could be combined, such as:

{ sleep 2; echo first finished; } & { sleep 3; echo second finished; } &

Bash being bash, there's often a multitude of different techniques to accomplish the same task, although sometimes with subtle differences between them.
