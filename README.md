# YouTrack Issue Downloader

A Python script that downloads all issues from a specified YouTrack project, including descriptions and comments in text as well as all attachments.
The issues are saved in a local directory structure with the ticket ID and subject in each folder's name.

## Features

- Downloads all issues from a specified YouTrack project
- Downloads issue descriptions, comments, and attachments
- Saves issues in a local directory structure
- Supports full refresh to re-download all issues

## Preliminaries

*Note:* Like any other python script, it is optional but recommended to run this script in a python virtual environment.

First, you need to install the required dependencies using pip:

```bash
pip install -r requirements.txt
```

You also need to set up a `.env` file in the same directory as your `main.py` file with the following variable:

- `YOUTRACK_TOKEN`: Your YouTrack permanent token. This is used for authentication when making requests to the YouTrack API.
- `YOUTRACK_PROJECT_ID`: The ID of the YouTrack project you want to download issues from.
- `YOUTRACK_URL`: The source

To facilitate the process, you can simply copy `.env.template` to `.env` and fill in the values for the above.

You can also add optional configuration by tweaking the following variables at the top of the `main.py` file:

- `ID_PAD_LENGTH`: This pads issue numbers for folder names, ensuring order. Increase if there are more than 999 issues in your project.
- `EXTENSION`: The file extension to use for attachments. For text-based projects, you can use "txt" or "md", but for projects with rich text, you may want to use "html".

## Usage

To run the script, simply execute the `main.py` file:

```bash
python main.py
```

By default, the script will skip issues that have already been downloaded. 
To force a full refresh and re-download all issues, you can set the `full_refresh` parameter to `True` when calling the `get_issues` function:

```python
get_issues(permanent_token, project_id=PROJECT_ID, full_refresh=True)
```

## Output

The script will create a directory named `exports` in the same directory as the `main.py` file. 
Inside this directory, it will create a separate directory for each issue, named with the issue's ID and summary. 
Each issue directory will contain a `content.txt` file with the issue's details and comments, and any attachments the issue may have.

## Filtering
If you have a custom field that disects something, you can narrow the list down
```
find -maxdepth 1 -execdir grep -qri 'fieldname:.*fieldvalue' {}  \; -print
```
