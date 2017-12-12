GTFS-ride is a new data standard looking to meet the needs of transit organizations to store and share their ridership data. It is a new standard, and input is encouraged to ensure the standard works for varying parties.

# Specification modification

## Quarterly reviews
GTFS-ride is dependent upon filesets created using the [GTFS specification](https://github.com/google/transit/tree/master/gtfs). Due to that dependency, quarterly reviews on the first business day of January, April, July, and October will occur to ensure ongoing compatibility. Any changes as a result of the review will be identified in the [Changelog](CHANGES.md#changelog).

## Discussion
Any modification to GTFS-ride may be discussed in the [GTFS-ride Changes Google Group](https://groups.google.com/forum/#!forum/gtfs-ride-changes). While starting a new topic discussing the desired change is not required for the change process, feedback received may ease the change's approval. 

## Initiated changes
There are multiple reasons why a change to GTFS-ride may occur: security vulnerability, usability defect, or new/improved feature sought. Depending on the change immediacy and method of change, the specification modification process will vary.

### Initiation
* If a change is desired, but the exact change to the code is not known, an [issue](https://github.com/ODOT-PTS/GTFS-ride/issues) should be opened. The current [authors](AUTHORS) will respond to the issue within 7 business days. An open issue presents an opportunity for collaboration between the authors and the community to craft a solution better serving GTFS-ride users. A branch will be created of the solution, and a pull request initiated.
* If a change is desired, and the exact change to the code is known, a branch should be created implementing the change where applicable (i.e. documentation, specification, etc.). The initiator of the change will create a pull request for the modified branch.

### Pull request
* Once a pull request is made, voting will occur for a minimum of 7 business days, and a new topic announcing the pull request must be posted to the [GTFS-ride Changes Google Group](https://groups.google.com/forum/#!forum/gtfs-ride-changes) the same day.
* During voting, any `-1` votes require the voting party to identify the reason for their vote and engage with the change seeking party to resolve.
* The change will be adopted only with a minimum of three `+1` votes and no outstanding `-1` votes. If the adoption threshold is not met at the end of day 7, the voting process continues until the threshold is met or the initiating party withdraws their pull request.

### Implementation
* For security or functionality changes, the modified branch will be merged into the master branch immediately upon approval of the pull request.
* For feature creation or enhancement changes, the modified branch will be merged into the master branch during the next quarterly review. This is done to provide some stability to the specification to ease development and adoption.

# Changelog

* `September 6, 2017` - Initial release.
* `January 1, 2018` - Quarterly review and new elements.
  * Added `load_count` to `board_alight.txt`
