# awesome-goggles
Awesome List for Goggles by Brave for Google, Bing, Baidu, Yandex, etc


### The original whitepaper / announcement
https://brave.com/wp-content/uploads/2021/03/goggles.pdf

### Goggles DSL

For the purpose of Goggles, we created a DSL (Domain SpecificLanguage) which will allow users to express rules able to capture flexible filtering logic applied on a large set of search results. This DSL needed to be plain text and self-contained to ease hosting and sharing, flexible enough to express fine-grained filtering logic of URLs and page features, yet sufficiently constrained so that filtering can be implemented in a very efficient way (as mentioned previ-ously, this system needs to be able to match thousands of candidate results against thousands of rules for each user query, without impacting latency in a perceivable way). Finally, it needed to be accessible enough so that even people without a technical background could quickly grasp its syntax and write rules, which would also encourage collaboration around the creation and curation of Goggles(e.g. communities)

A list of filters, or Goggle, is a self-contained text file where each line can contain a filter (empty lines or comments—line starting with a ’!’ character—are ignored). Ranking of search results will be altered based on the filters contained in the file. Each filter is composed of two parts: a trigger and an action, separated by a $ character: `<trigger>$<action>`. The trigger part is a pattern which needs to match a result candidate. 

It can leverage the following features:
- **Plain Patterns:** allow targeting a URL (or another result attribute like its title) based on a string of characters which it should contain. The filter "/coronavirus-" would trigger on any URL containing this specific string of characters (example: https://example.com/coronavirus-update.html)
- **Wildcard Patterns:** extend plain patterns with globbing capabilities: the special symbol "*" can be used to match any number of characters. Filter "/health/*/coronavirus-" would match any URL containing the substring "/health/", followed by zero or more characters, then "/coronavirus-" (example: https://example.com/health/2020/coronavirus-update.html)
- **Left and Right Anchors:** introduce a special "|" character which, when appearing at the start or end of a filter, forces a pattern to match the beginning or end of a URL. Filters "|https://" and ".html|" would match URLs starting with https:// or ending with .html, respectively.

Each filter can also be annotated with additional options (following the "$" character). Multiple options can be specified at the same time, and separated by comas. We leverage this syntax to add ways to further fine-tune the behaviour of Goggles; either to specify which features of a result candidate should be considered (i.e.target), or how the ranking should be affected (i.e. action).

#### Goggles Syntax Examples / Filters
- **$boost=XX** is used to alter the ranking of specific results by XX (e.g. $boost=1 would  not alter the ranking, while $boost=2 would make a result two times more important)
- **$discard** completely drops candidates from the list of results

Filtering based on specific attributes of the result page can be achieved with:
- **$lang=XX** to target the language.
- **$inurl** to target the URL
- **$inquery** to target queries leading to a candidate.
- **$intitle** to target the title.
- **$indescription** to target the description.
- **$intext** to target the full content.

Last but not the least, these features can all be combined to form complex filters. For example, the filter: `/news/*/covid.html|$inurl` would match candidates based on their URL. This description is by no means complete or final, and we will release a specification of the language once it is stabilized.


## Awesome Goggles Resources

### Original Paper / Announcement:
- [Goggles Whitepaper](https://brave.com/wp-content/uploads/2021/03/goggles.pdf)
- [Brave Search Announcement HN](https://news.ycombinator.com/item?id=27593360)
