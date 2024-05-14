@Library('roboshop-shared-library') _
def configmap [
    application: "nodejsvm"
    component: "catalogue"
]
echo "hello true"
if(!env.branch_name.ignorecase('main'))
{
    pieplinedecission.buildpipeline(configmap)
}
else
{
    echo "main branch" 
}