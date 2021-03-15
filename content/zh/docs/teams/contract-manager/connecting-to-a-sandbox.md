---
title: 连接到沙箱
weight: 1
---

请注意，本文档的这一部分假定您已经创建了一个沙箱并将合同部署到该沙箱。
如果您需要帮助，请开始使用沙箱和将其部署到沙箱, 请查看[创建沙箱](/docs/teams/sandboxes/creating-a-sandbox)部分和[部署到沙箱](/docs/teams/deployments/deploying-to-a-sandbox)部分以了解更多详细信息。

如果您将合同部署到沙盒，并希望使用合同管理器与其进行交互，则需要将 MetaMask 连接到沙盒实例。
要将 MetaMask 连接到沙盒，您需要 RPC URL 和生成的助记符。
Navigate to **<span class="inline-menu-item"><i class="far fa-cubes"></i>SANDBOXES</span>** and click on <span class="inline-button">VIEW/EDIT</span> of the sandbox you deployed to.
Copy the **Mnemonic**, open your MetaMask browser extension, and select **Import using account seed phrase**.

<figure class="screenshot">
  <img class="img-fluid" src="/img/docs/teams/contract-manager-03.png" title="Sandbox view/edit modal and MetaMask wallet setup" alt="Sandbox view/edit modal and MetaMask wallet setup" />
  <figcaption class="text-center">Sandbox view/edit modal and MetaMask wallet setup</figcaption>
</figure>

A new tab will open for restoring your account with a seed phrase/mnemonic; paste the mnemonic into the **Wallet Seed** text box, create a password, and click **Restore**.

<figure class="screenshot">
  <img class="img-fluid" src="/img/docs/teams/contract-manager-04.png" title="Restore MetaMask account with seed phrase" alt="Restore MetaMask account with seed phrase" />
  <figcaption class="text-center">Restore MetaMask account with seed phrase</figcaption>
</figure>

Once you have successfully logged into MetaMask via seed phrase, next you'll need to create a custom RPC using the sandbox RPC URL.
Copy the **RPC URL**, open your MetaMask browser extension, click on the Network dropdown list, select **Custom RPC** from the bottom of the list.
Enter a network name, paste the RPC URL into the **New RPC URL** text box, enter in Ganache's Chain ID: `1337`, and any other relevant information, and click **Save**.

<figure class="screenshot">
  <img class="img-fluid" src="/img/docs/teams/contract-manager-05.png" title="Create Custom RPC in MetaMask" alt="Create Custom RPC in MetaMask" />
  <figcaption class="text-center">Create Custom RPC in MetaMask</figcaption>
</figure>

If you click on the MetaMask logo it'll take you back to your account details where you should see a test account with 100 ETH.
Now you're connected to MetaMask and can head over to the contract manager to interact with your contract.

Navigate to the **<span class="inline-menu-item"><i class="fal fa-parachute-box"></i>DEPLOYMENTS</span>** page, toggle to **TABLE** view, and select the deployment from your list of deployments.
On the chosen deployment page, under the **CONTRACTS** tab, you can chose a contract to interact with by clicking on **<span class="inline-button"><i class="far fa-pager"></i> MANAGE</span>**.

A MetaMask pop-up will appear asking you to select an account to use, choose which account to use from the list and click **Next**, and finally accept the permissions by clicking **Connect**.
You've successfully selected an account, now you're ready to interact with the contract manager! To learn more on interacting with contracts, head over to the <a href="/docs/teams/contract-manager/interacting-with-functions">Interacting with functions</a> section.
