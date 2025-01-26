# AIV File Format

The `.AIV` file format is used in the Stronghold Crusader game to store AI village data. This file format consists of multiple sections, each containing specific data related to the AI village. Below is a detailed breakdown of the `.AIV` file format.

## Table of Contents
- [AIV File Structure](#aiv-file-structure)
- [Sections](#sections)

## AIV File Structure

| Offset | Number of Bytes | Name                        | Description                                                                 |
|--------|-----------------|-----------------------------|-----------------------------------------------------------------------------|
| 0      | 4               | `directory_size`            | Size of the directory.                                                     |
| 4      | 4               | `size`                      | Total size of the AIV file.                                                |
| 8      | 4               | `sections_count`            | Number of sections in the AIV file.                                        |
| 12     | 4               | `version_number`            | Version number of the AIV file.                                            |
| 16     | 16              | `directory_u1`              | Unknown data (4 integers).                                                 |
| 32     | 400             | `section_uncompressed_lengths` | Uncompressed lengths of each section (100 integers).                       |
| 432    | 400             | `section_lengths`           | Lengths of each section (100 integers).                                    |
| 832    | 400             | `section_indices`           | Indices of each section (100 integers).                                    |
| 1232   | 400             | `section_compressed`        | Compression flags for each section (100 integers).                         |
| 1632   | 400             | `section_offsets`           | Offsets of each section (100 integers).                                    |
| 2032   | 4               | `directory_u7`              | Unknown data.                                                              |
| 2036   | Variable        | `sections`                  | Data of each section, starting at the offsets specified in `section_offsets`. |

## Sections

Each section in the AIV file contains specific data related to the AI village. The sections are identified by their indices and can be either compressed or uncompressed. Below are some of the known sections:

### Section 2004
- **Description**: Contains data for a specific part of the AI village.
- **Data Type**: Compressed

### Section 2007
- **Description**: Contains construction data for the AI village.
- **Data Type**: Compressed
- **Data Format**: 100x100 matrix of `uint16` values.

### Section 2008
- **Description**: Contains build steps for the AI village.
- **Data Type**: Compressed
- **Data Format**: 100x100 matrix of `uint32` values.

### Section 2010
- **Description**: Contains the step count for the AI village.
- **Data Type**: Uncompressed
- **Data Format**: Single `uint32` value.

### Section 2011
- **Description**: Contains pause data for the AI village.
- **Data Type**: Uncompressed
- **Data Format**: Array of 50 `int32` values.

### Section 2012
- **Description**: Contains unit data for the AI village.
- **Data Type**: Uncompressed
- **Data Format**: 24x10 matrix of `int32` values.

### Section 2014
- **Description**: Contains the pause delay amount for the AI village.
- **Data Type**: Uncompressed
- **Data Format**: Single `int32` value.

For more detailed information on each section and how to manipulate the data, refer to the [sourcehold-maps documentation](https://github.com/sourcehold/sourcehold-maps/wiki)
