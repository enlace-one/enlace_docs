# SOCX Command Line Tool Version History

## Version 2.5.1 

Published to pypi.org: 21 June 2026

Published to test.pypi.org: 21 June 2026

Major bug fixes in new packing and deployment method and unified syntax for combine and awake. Reintroduced the awake restart flag.

## Version 2.5.0

Published to pypi.org: 20 June 2026

Published to test.pypi.org: 20 June 2026

Includes many syntax changes as the package shifted to using the Typer interface. Other changes include:
- The find command's smart search now iterates through folders in reverse starting from cwd and ignoring anything previously searched
- There is a new command called Configure-pip which sets the minimum package day to 14 days and sets trusted hosts. This is to help reduce the concern of malicious packages. 

## Version 2.4.1

Published to pypi.org: N/A

Published to test.pypi.org: 2 November 2025

Added the unzip action which can unzip several zips into the directory they reside in.

## Version 2.4.0
Published to pypi.org: 1 November 2025

Published to test.pypi.org: 1 November 2025

Added dependencies so they are installed automatically when SOCX is. 

Fixed safelinks unwrapping. 

Added --deduplicate flag to combine

## Version 2.3
Published to pypi.org: 9 August 2025

Published to test.pypi.org: 9 August 2025

### Awake Function
Introduced the --restart flag

### Combine CSVS Function
Fixed the --skip_og_filename_column flag

### Find Function 
Fixed the --skip_smart flag

## Version 2.2
Published to pypi.org: 17 July 2025

Published to test.pypi.org: 17 July 2025

### Awake Function
Intruduced the function