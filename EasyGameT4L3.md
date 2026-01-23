## Manage Cloud Storage Lifecycle Policy using gcloud storage

Expertly crafted by Easy Game

### Creator Chinu Bhai
- **Use the code to complete the lab quickly without any issue and manual hard work.**


### Run the following Commands in CloudShell

```bash
PROJECT_ID=$(gcloud config get-value project)
cat <<EOF > lifecycle.json
{
  "rule": [
    {
      "action": {
        "type": "SetStorageClass",
        "storageClass": "NEARLINE"
      },
      "condition": {
        "daysSinceNoncurrentTime": 30,
        "matchesPrefix": ["projects/active/"]
      }
    },
    {
      "action": {
        "type": "SetStorageClass",
        "storageClass": "NEARLINE"
      },
      "condition": {
        "daysSinceNoncurrentTime": 90,
        "matchesPrefix": ["archive/"]
      }
    },
    {
      "action": {
        "type": "SetStorageClass",
        "storageClass": "COLDLINE"
      },
      "condition": {
        "daysSinceNoncurrentTime": 180,
        "matchesPrefix": ["archive/"]
      }
    },
    {
      "action": {
        "type": "Delete"
      },
      "condition": {
        "age": 7,
        "matchesPrefix": ["processing/temp_logs/"]
      }
    }
  ]
}
EOF
gsutil lifecycle set lifecycle.json gs://$PROJECT_ID-bucket
```

### Congratulations !!!!

Congrulations Your Lab is completed Successfully.

[![YouTube](https://img.shields.io/badge/Subscribe-FF0000?style=for-the-badge&logo=youtube&logoColor=white)](https://www.youtube.com/@Chinmay_Joshi-CJ?sub_confirmation=1)  
