node('Dotnetcore')
{
    stage('SCM')
    {
        checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/mnyaqoub/pi.git']]]);
    }

    stage('Build')
    {
        sh 'dotnet build ./src/Pi.Web/Pi.Web.csproj'
    }

    stage('Test')
    {
        echo 'Excute unit tests'
        dotnet test --logger "trx;LogFileName=/out/Pi.Math.trx" ./Pi.Math.Tests/Pi.Math.Tests.csproj
        dotnet test --logger "trx;LogFileName=/out/Pi.Runtime.trx" ./Pi.Runtime.Tests/Pi.Runtime.Tests.csproj
    }

    stage('Package')
    {
        echo 'Zip it up'
    }

    stage('Deploy')
    {
        echo 'Push to deployment'
    }

    stage('Archive')
    {
        archiveArtifacts artifacts: 'dotnetwebapp/*.*'
    }
}
