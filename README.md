
<img src="https://raw.githubusercontent.com/phil1436/node-red-contrib-iris/master/src/InterSystemsLogo.png" width = "200">
<h1>node-red-contrib-iris</h1>
<details>
    <summary><b>General</b></summary>
    <p>
       An interface for <a href = 'https://nodered.org/'>Node-RED</a> to <a href = 'https://www.intersystems.com/data-platform/'>InterSystems IRIS Data Platform</a>.
    </p>
</details>

<details>
    <summary><b>Required</b></summary>
    <p>
        <ul>
            <li><a href="https://docs.intersystems.com/irislatest/csp/docbook/DocBook.UI.Page.cls?KEY=PAGE_nodejs_native">Native API</a> (v 1.2.0) installed in Node-RED.</li>
            <li><a href = "https://github.com/phil1436/node-red-iris/tree/master/ObjectScript">Node.IRISInterface</a> (v 1.3) class installed in Intersystems IRIS.</li>
        </ul>
    </p>
</details>

<details>
    <summary><b>Install</b></summary>
    <p>
       Either use the <i>Node-RED Menu - Manage Palette - Install</i>, or run the following command in your Node-RED user directory - typically <code>~/.node-red</code>

```shell
npm i node-red-contrib-iris
``` 
    
</p>
</details>

<details>
    <summary><b>Import Native API</b></summary>
    <p>
        In <code>~/.node-red/settings.js</code> add module in (already existing) <code>functionGlobalContext</code>:
        
<pre>
functionGlobalContext: {
    // os:require('os'),
    iris:require('./node_modules/node-red-contrib-iris/intersystems-iris-native')
}
</pre>

You can find the API package under <code>.node-red/node_modules/node-red-contrib-iris/intersystems-iris-native</code>. Please check the <a href = "https://github.com/phil1436/node-red-contrib-iris/blob/master/intersystems-iris-native/README.md">README</a> file for supported operating systems. If your OS is not supported you can get the API from your Intersystems IRIS instance under: <code>~/IRIS/dev/nodejs/intersystems-iris-native</code>.

See the <a href = "https://nodered.org/docs/user-guide/writing-functions#loading-additional-modules">documentation</a> for how to load additional modules into Node-RED.
</p>
</details>

<details>
    <summary><b>Download Node.IRISInterface</b></summary>
    <p>
        Go to <a href = 'https://raw.githubusercontent.com/phil1436/node-red-contrib-iris/master/ObjectScript/Node.IRISInterface.cls'>raw.githubusercontent</a>. Do a right click on the page and choose <i>Save Page As...</i> . Afterwards go to the InterSystems Management Portal and navigate to <i>System Explorer > Classes</i> and click on <i>Import</i>. There you select the file you just downloaded and click <i>Import</i>.<br>
         When you only operate in one namespace, import the class into this namespace. When you have multiple namespaces you want to have access to, <a href = "https://docs.intersystems.com/iris20221/csp/docbook/DocBook.UI.Page.cls?KEY=GSA_config_namespace#GSA_config_namespace_addmap_all">map the class to namespace %ALL</a>.
    </p>
</details>

<details>  
    <summary><b>Connect to IRIS</b></summary>
    <p>
        Set connection properties via the node properties. The Node will build a connection when you deploy and will hold that connection up until you redeploy or disconnect manually.
    </p>
        <img src = "https://raw.githubusercontent.com/phil1436/node-red-contrib-iris/master/src/NodeProps.png" width = "400">
    <p>
    You can set the default properties in <code>~/.node-red/node_modules/node-red-contrib-iris/ServerProperties.json</code>. Or use the <a href = "https://github.com/phil1436/node-red-contrib-iris/blob/master/examples/SetServerProperties.json">SetServerProperties flow</a> under <i>Import > Examples > node-red-contrib-iris > SetServerProperties</i>.
    </p>
</details>

<details>  
    <summary><b>Usage</b></summary>
    <p>
         The nodes are secure against SQL injection by parametrize the statements.
    </p>
    <p>
         Pass the SQL statement as a string in the <b>msg.data</b> field and the nodes will parameterize the statement itself.
    </p>
<pre>
msg.data = "SELECT * FROM NodeRed.Person WHERE Age >= 42 AND Name = 'Max' "
</pre>
Or parameterized statement:
<pre>
msg.data = { 
    "sql": "SELECT * FROM NodeRed.Person WHERE Age >= ? AND Name = ? ",
    "values": [42, "Max"]
}
</pre>
</details>

<details>
    <summary><b>Nodes</b></summary>
    <p>
        <ul>
            <li><b>IRIS</b>: A Node for executing DML statements such as SELECT, UPDATE, INSERT and DELETE and DDL statements such as CREATE, ALTER and DROP in Intersystems IRIS.</li>
            <li><b>IRIS_CREATE</b>: Creates a class in Intersystems IRIS.</li>
            <li><b>IRIS_DELETE_CLASS</b>: Deletes a class in Intersystems IRIS.</li>
            <li><b>IRIS_INSERT</b>: A Node for only SQL-INSERT-Statements. Can also generate the class, if it does not already exists, based on the statement.</li>
            <li><b>IRIS_OO</b>: Can insert a hierarchical JSON-Object.</li>
            <li><b>IRIS_CALL</b>: Call Intersystems IRIS classmethods.</li>
        </ul>
    </p>
    <img src = "https://raw.githubusercontent.com/phil1436/node-red-contrib-iris/master/src/NodesOverview.png" width = "200">

<p> See Node description for further informations.</p>
</details>

<details>
    <summary><b>Bugs</b></summary>
    <p>
        <ul>
            <li>Currently does not work in Docker Container!</li>
            <li>The statement will be parametrized wrong if whitespaces and commas used in strings. Please parametrize the Statement before. Example:<br>
Does not work:
<pre>
msg.data = "SELECT * FROM NodeRed.Person WHERE Name = 'Smith, John'"
</pre>
Will work:
<pre>
msg.data = {
    "sql":"SELECT * FROM NodeRed.Person WHERE Name = ?,
    "values":["Smith, John"]
    }
</pre>
            </li>
        </ul>
    </p>
</details>

<p>
<br>
<a href= "https://www.npmjs.com/package/node-red-contrib-iris">npm</a><br>
<a href= "https://github.com/phil1436/node-red-contrib-iris">GitHub</a><br>
<a href= "https://flows.nodered.org/node/node-red-contrib-iris">nodered.org</a><br>
<a href= "https://github.com/phil1436/node-red-contrib-iris/blob/master/CHANGELOG.md">CHANGELOG</a><br>
<a href= "https://community.intersystems.com/post/intersystems-iris-integration-node-red">InterSystems Developer Community</a>
</p>
<br>
<p>by Philipp Bonin<br>Powered by <a href= "https://www.intersystems.com/" style="color: #00b4ae">InterSystems</a>.</p>