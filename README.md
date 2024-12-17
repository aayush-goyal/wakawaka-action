# WakaWaka - Coding Stats GitHub Action

**WakaWaka - Coding Stats GitHub Action** is a simple and easy-to-use GitHub Action. [**WakaTime**](https://wakatime.com), allows developers to access and display their coding activity data in various visual formats. Whether you want to show coding stats as badges or generate rich charts to display your activity, this action can do it all. You can use the generated output directly on your GitHub profile.

# Features
- **Stats**: Generate shield badges for various coding stats.
- **Charts**: Visualize coding activity data in different chart formats including bar charts, pie charts, and more.
- **Customization**: Customize the type and range of charts and badges to suit your needs.

# How the Action Works

The action interacts with this **[WakaTime API Wrapper](https://github.com/aayush-goyal/wakawaka)** to retrieve data from your WakaTime account. It fetches your coding stats and generates dynamic charts and badges based on this data. These charts and badges are then displayed directly in your GitHub profile or any markdown-supported platform.

# Workflow
1. **Authentication**: You provide your WakaTime `username` and `auth_token`. The action uses these to access your WakaTime data.
2. **Data Retrieval**: The action makes requests to the wrapper's API endpoints to retrieve data based on your specified parameters (e.g., stat type, chart type, and etc). Refer to [WakaWaka API](https://github.com/aayush-goyal/wakawaka/blob/master/README.md) docs to know more.
3. **Chart Generation**: The APIs can generate different types of charts such as bar charts, pie charts, and doughnut charts, depending on the data you wish to display.
4. **Badge Creation**: The APIs can also create shield-style badges that can be added to your README to highlight your activity.
5. **Display**: Once the charts and badges are generated, the action updates your GitHub profile with the visual content.

# How to Use the Action
## Prerequisites
Before you can use the **Wakawaka GitHub Action**, you’ll need the following:
- A **WakaTime** account (sign up at [WakaTime](https://wakatime.com/)).
- Your **WakaTime API token**: You can get this token by visiting this [aayushgoyal - WakaWaka](https://aayushgoyal.in/wakawaka).

**NOTE:** Once you have generated the toke, copy and save it as you will need it later.

## Setup
1. **Add the Action to Your GitHub Repository**: Add the following YAML snippet to your repository's `.github/workflows` folder (e.g., `update-wakastats.yml`):
```  
name: WakaTime Readme

on:
  schedule:
    - cron: "30 18 * * *"   # Runs everyday 12AM IST.
  push:
    branches:
      - "**"

jobs:
  waka_waka_job:
    runs-on: ubuntu-latest
    name: A job to update Wakatime stats in README.
    steps:
      - name: Checkout
        uses: actions/checkout@v4
      - name: WakaWaka Action
        uses: aayush-goyal/wakawaka-action@v1.2.3

        with:
          COMMIT_EMAIL: "your_primary_email_with_GitHub"
          GH_ACTOR: ${{ github.actor }}
          GH_TOKEN: ${{ secrets.GITHUB_TOKEN }}
          GH_WORKSPACE: ${{ github.workspace }}
          WAKA_AUTH_TOKEN: ${{ secrets.WAKATIME_API_KEY }} #API token you saved earlier.
          WAKA_USERNAME: "your_wakatime_username"

```
2. **Set Up Secrets**: In your GitHub repository, navigate to `Settings > Secrets` and add the following secrets:

    -   `WAKATIME_API_KEY`: Your WakaTime API token.

Your action is now ready to use on your GitHub README profile. All you need to is to use special Markdown comments to start customizing the profile.

## Using Action on GitHub Profile

WakaWaka works with special comments you define in the Markdown README file. To tell WakaWaka to insert either a stat or a chart you need three comments one after another on separate lines as shown below:
```
<!-- WAKAWAKA_START -->
<!-- WAKAWAKA_CONFIG__OPTION --> [1]
<!-- WAKAWAKA_END -->
```

### Badges
Currently, WakaWaka supports only two types of badges:
1. Best Coding Day

    Replace `[1]` with `<!-- WAKAWAKA_CONFIG__STATS_BEST_DAY -->`

    WakaWaka will automatically get the badge and insert it just below the [1] comment in your README file.

2. Daily Coding Average
    
    Replace `[1]` with `<!-- WAKAWAKA_CONFIG__STATS_DAILY_AVG -->`

### Charts
You can do a lot more when it comes to charts on WakaWaka.

The basic comment for customizing the chart is as follows:

Replace `[1]` with
`<!-- WAKAWAKA_CONFIG__ST={st_digit}&CT={ct_digit}&DT={dt_digit}&R={range_digit} -->`

Here is the breakdown of all the digits you can pass to this customization comment for generating beautiful charts on your GitHub Readme profile.

#### `st_digit`
1. `0` → Programming Languages
2. `1` → Categories
3. `2` → Editors
4. `3` → OS
5. `4` → Projects

#### `ct_digit`
1. `0` → Bar Chart Horizontal
2. `1` → Bar Chart Vertical
3. `2` → Doughnut Chart
4. `3` → Nightingale Chart
5. `4` → Pie Chart

### `dt_digit`
1. `0` → Percent
2. `1` → Time

#### `range_digit`
1. `0` → Last 7 Days
2. `1` → Last 30 Days
3. `2` → Last 6 Months
4. `3` → Last Year
5. `4` → All Time

Based on the combinations you can generate almost all the kind of charts you would need based on your coding stats. For example, let us assume a programmer wants to display his editor stats in a doughnut chart, but only for the last 30 days. Here is the config comment he needs to put in his README file:
```
<!-- WAKAWAKA_START -->
<!-- WAKAWAKA_CONFIG__ST=2&CT2=&DT0=&R=1 -->
<!-- WAKAWAKA_END -->
```

You can also visit [WakaWaka - API](https://aayushgoyal.in/wakawaka) repo to learn more about the APIs the action uses behind the scenes and to play with them.

# Future Plans
Here’s a look at some of the exciting features I plan to implement in the future:

- **More chart types**: Add more types of charts (e.g., line charts, stacked bar charts, etc.).
- **More stats**: More stats from your coding activity like time when you are most coding, your best month for coding, and etc.
-   **Customization options**: Provide more options for customizing the appearance and behavior of charts and badges (e.g., colors, sizes, themes).
-   **Integration with other platforms**: Extend the functionality to support more platforms like GitLab, Bitbucket, etc.
-   **Enhanced data analytics**: Provide deeper insights into your coding activities, such as trends over time, comparison between projects, etc.

If you want to contribute to the project, please read [CONTRIBUTING](https://github.com/aayush-goyal/wakawaka-action/blob/main/CONTRIBUTING.md).

# License
This project is licensed under the [MIT License](https://opensource.org/license/mit) - see the [LICENSE](https://github.com/aayush-goyal/wakawaka-action/blob/master/LICENSE) file for details.

# Contact
For further questions, feel free to reach out via [GitHub Discussions](https://github.com/aayush-goyal/wakawaka-action/discussions/).

Let me know if you want further customization or any additional sections!
