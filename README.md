# helm-charts


Update helm chart

# Package the chat

    helm package $name -d .\$chart_directory

# Index the chart directory

    helm repo index .\helm-charts\

# Push all changes to github

# Add Git repo

    helm repo add elros https://elros-virtual.github.io/helm-charts/

# Update local repo

    helm repo update

# To list repos

    helm repo list

# To see what is inside of the repo

    helm search repo elros

# If needed remove repo 

    helm repo remove elros



