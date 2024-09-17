---
draft: false
title: "Web scraping a site with embedded JSON"
date: 2019-01-23
slug: web-scraping-embedded-json
categories:
  - data science
tags:
  - meta data science
---

[code snippet](https://github.com/sethschori/scraping/blob/master/scripts/cleantech100.py#L41-L92)

```python
def scrape_list():
    """Scrape the cleantech list and put companies into a list of dicts."""
    cleantech100_url = 'https://i3connect.com/gct100/the-list'
    cleantech100_base_url = 'https://i3connect.com'
    request = requests.get(cleantech100_url)
    bs = BeautifulSoup(request.content, "html.parser")
    table = bs.table
    # The HTML table has the headers: COMPANY, GEOGRAPHY, FUNDING, SECTOR,
    # YEAR FOUNDED
    header = [
        'cleantech_url',     # from COMPANY
        'company_country',   # from GEOGRAPHY
        'company_funding',   # from FUNDING
        'company_sector',    # from SECTOR
        'company_year_founded',  # from YEAR FOUNDED
        'company_region',    # Column exists but is not displayed in the header.
        'company_video'      # Column exists but is not displayed in the header.
    ]
    companies = []
    for row in table.tbody.find_all('tr'):
        company = {}
        index = 0
        if 'id' in row.attrs and row.attrs['id'] == 'gct-table-no-results':
            # Last row of table should be skipped because it's just got this:
            # <tr id="gct-table-no-results">
            #           	<td colspan="7">No results found.</td>
            continue
        for cell in row.find_all('td'):
            # co_key is the key to use within company dict,
            # e.g. company[co_key] could point to company['cleantech_url']
            co_key = header[index]
            if cell.string is None:
                # The first and last columns of the HTML table have no text
                # (cell.string is None).
                try:
                    # The first column of the HTML table holds a link to the
                    # company detail page. This is handled by the try statement,
                    # as there is an `href` attribute within the <a> tag.
                    company[co_key] = cleantech100_base_url + cell.a.get('href')
                except AttributeError:
                    # The last column of the HTML table holds iframe links to
                    # videos. Therefore, there is no <a> tag within the cell,
                    # only a <span> element with a 'data-video-iframe' element.
                    # This is handled by the except statement.
                    video_url = cell.span.get('data-video-iframe')
                    if len(video_url) > 10:
                        company[co_key] = video_url
            else:
                company[co_key] = cell.string
            index += 1
        companies.append(company)
    return companies
```