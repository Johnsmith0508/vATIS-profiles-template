# vATIS Profile Generator
This repository is designed to simplify management of multiple vATIS profiles that contain overlapping airports. An update to an airport only needs to be made once, and when the next version is released, that change will be applied to all profiles that contain that airport.

## Getting Started
- Click "Use this template" at the top of this repository to create a repository based on this one.
- Export each airport in vATIS as a `.station` file.
- Place individual station files in the root directory of the repository, and profile templates in the `profiles/` directory.
> [!NOTE]
> Individual station files must end in `.station`, and profile templates should be named the same as the desired output files.

## Configuring Profiles
The build config file is located in `.github/build/config.json`. Each vATIS profile is defined by an entry in the profiles object, where the key is the profile name, and the value is an array of ICAO codes of airports to be included in that profile.

Arrival and departure ATISes can be represented with the `_A` and `_D` suffixes, respectively.

The prefix field is applied to all profile file names. For example if you wish all of your file names to be of the form `vATIS_Profile_ZNY_{profile name}`, you can set the prefix to `vATIS_Profile_ZNY_`

> [!NOTE]
> Spaces should be avoided in profile names, as these are replaced by `.` when the file is uploaded to Github.

A prepopulated config is present in this repository's [.github/build](.github/build/config.json) folder.

## Profile Templates
Profiles in the `profiles/` directory should be named identically to how you wish the generated profiles to be named.

When the build script runs, individual stations are added to each template, as defined in the config file. Because of this, it is not necessary to have any stations defined in the template. 

To have vATIS automatically check for updates from your github repository, you can set the updateUrl to `https://github.com/{username}/{reponame}/releases/latest/download/{filename}.json`

An example profile template is provided below:

```JSON
{
  "name": "ZNY N90",
  "id": "67c61fde-6ea4-4bd6-a22c-500ae8101bab",
  "updateUrl": "https://github.com/nyartcc/facility-vatis/releases/latest/download/vATIS_Profile_ZNY_N90.json",
  "updateSerial": 1970010101,
  "stations": [],
  "version": 4
}
```

## Running a Build
The action is configured to run whenever a new release is created on Github. Simply create and publish a new release with no attached files. About 30 seconds later, the completed profiles will be added as assets to that release. The action will also run when a new tag is pushed to the repository, at which point a new release will be created.
