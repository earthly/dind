VERSION --wildcard-builds 0.8

PROJECT earthly-technologies/core

# test runs tests for all defined dind images in this repo
test:
    BUILD --pass-args ./os/*+test-build

# release expects to get a renovate branch in the form of renovate/<os>-dind-image, extracts the os and then kicks off its +release target
# this is meant to be run by a github workflow
release:
    FROM alpine
    # RENOVATE_BRANCH is the renovate branch that is expected to get merged and trigger this target
    ARG --required RENOVATE_BRANCH
    LET os=${RENOVATE_BRANCH#renovate/}
    SET os=${os#major-}
    # using a LET/SET in the target path does not work, use an ARG instead until it's fixed
    ARG OS=${os%-dind-image}
    BUILD --pass-args ./os/$OS+release
