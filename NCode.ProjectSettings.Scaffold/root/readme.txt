After this package is installed, perform the following to complete the project scaffold:

    1) Build the Solution

    2) Add the following to 'Solution Files':

        .editorconfig
        .gitattributes
        .gitignore
        COPYRIGHT.txt
        LICENSE.txt
        README.md

    3) Open $(ProjectName).csproj and edit:

        From:
            <PackageReference Include="NCode.ProjectSettings.Scaffold" Version="1.0.6" />

        To:
            <PackageReference Include="NCode.ProjectSettings.Scaffold" Version="1.0.6" >
                <PrivateAssets>All</PrivateAssets>
            </PackageReference>

        Reference:
            https://github.com/NuGet/Home/issues/4125
