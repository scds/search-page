# search-page

A widget to easily search and explore SCDS workshops.

## Purpose

This repository contains a GitHub site of a search widget so that other websites (like scds.ca) can embed it into their pages.

There's an interactive search page version, as well as a non-interactive static text-only page.

## How to Use

### Adding to a page

To add the search widget to an SCDS WordPress page, use a shortcode block and include the following line:  
```[iframe src="https://learn.scds.ca/search-page/" width="100%" scrolling="yes" height="850px" ]```

To add the search widget to any other page, use the following iframe code:  
```html
<iframe src="https://learn.scds.ca/search-page/" width="100%" scrolling"yes" height="850px">
</iframe>
```

Currently, there's no support to add the text-only page as an automatically resizable widget.

### Adding/updating Workshops

To add or update the workshops that are listed in the tool, you have to modify `_data/workshop_list_scratch.csv`. If there are new series added, `_data/workshop_series.json` must be modified as well.

To modify the CSV, the easiest thing would be to open it in a supporting spreadsheet application (something like Excel can work). From here, you'll see 8 columns: Title, Year, URL, Image, Series, Type,Topic, Software.

- Title: The name of the workshop. Ensure that this does not conflict with any other workshop name. If it does, add the year into the name.
    - Ex: Intermediate Python Programming (2022-2023) vs Intermediate Python Programming (2023-2024)
- Year: The year(s) that the workshop was offered. If the webpage has multiple years of the workshop offered, separate options by a semicolon (;) with no spaces.
    - Ex: `2022-2023;2023-2024` means that the workshop page has recordings for the 2022-2023 year as well as the 2023-2024 year.


## Credits

Made by Richie Motorgeanu.