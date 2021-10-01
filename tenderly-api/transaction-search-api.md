# Transaction Search API

## API Authentication

You can read more about API authentication here: [Authenticating with the Tenderly API](authenticating-with-the-tenderly-api.md).

## Transaction Search API

Endpoint:  
  
`https://api.tenderly.co/api/v1/account/{{username}}/project/{{project-slug}}/transactions?page=1&perPage=20`

Get parameters:

<table>
  <thead>
    <tr>
      <th style="text-align:left">Name</th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left">Mandatory Y/N</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">page</td>
      <td style="text-align:left">number</td>
      <td style="text-align:left">the page of the transaction results</td>
      <td style="text-align:left">N</td>
    </tr>
    <tr>
      <td style="text-align:left">perPage</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">number of txs to return</td>
      <td style="text-align:left">N</td>
    </tr>
    <tr>
      <td style="text-align:left">status</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">true &#x2192; returns successful txs
        <br />
        <br />false &#x2192; returns failed txs if nothing is passed returns all txsYY</td>
      <td
      style="text-align:left">N</td>
    </tr>
    <tr>
      <td style="text-align:left">txType</td>
      <td style="text-align:left">string[]</td>
      <td style="text-align:left">internal &#x2192; returns only internal txs
        <br />
        <br />direct &#x2192; returns only direct txs if nothing is passed returns all
        txs</td>
      <td style="text-align:left">N</td>
    </tr>
    <tr>
      <td style="text-align:left">contractId[]</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">
        <p>array of contract ids contract ids are in the format of:</p>
        <p>eth:{{network_id}}:{{lowercase_addr}}
          <br />
          <br />Note: the id must be the part of the projectN</p>
      </td>
      <td style="text-align:left">N</td>
    </tr>
    <tr>
      <td style="text-align:left">functionSelector</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">the function selector of the functionN</td>
      <td style="text-align:left">N</td>
    </tr>
    <tr>
      <td style="text-align:left">after</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">ISO8601 date</td>
      <td style="text-align:left">N</td>
    </tr>
    <tr>
      <td style="text-align:left">before</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">ISO8601 date</td>
      <td style="text-align:left">N</td>
    </tr>
  </tbody>
</table>

