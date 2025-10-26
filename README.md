# Puppets NFT - Admin Dashboard

A web-based admin dashboard for managing and claiming royalty rewards from the Puppets NFT collection on Sui blockchain.

## Features

- **Royalty Claim**: One-click withdrawal of accumulated royalties from secondary sales (~23.43 SUI available)
- **Real-time Balance**: Live display of royalty balance from TransferPolicy
- **Collection Stats**: View minting statistics across all phases
- **Treasury Monitoring**: Monitor the treasury wallet balance
- **Direct Explorer Links**: Quick access to all contract objects on SuiScan

## Quick Start

### Option 1: Deploy to Vercel (Recommended)

[![Deploy with Vercel](https://vercel.com/button)](https://vercel.com/new/clone?repository-url=https://github.com/corey-beep/sui-puppets-claim)

1. Click the "Deploy with Vercel" button above
2. Connect your GitHub account
3. Deploy (takes ~30 seconds)
4. Visit your deployed site
5. Connect with Sui Wallet that owns the TransferPolicyCap
6. Click "Claim Royalties"

### Option 2: Local Development

```bash
# Clone the repository
git clone https://github.com/corey-beep/sui-puppets-claim.git
cd sui-puppets-claim

# Open in browser
open index.html
```

## Important Contract IDs

| Object | Address |
|--------|---------|
| **Package** | `0xefb46efef2715424b184462c4e3c831456909efe2fbe72b20e4f80e1bd80ce03` |
| **NFTCollection** | `0x551188baec211f18e0fb58fa78adfe7ce8eb695bcb545ef2206d7b20a2f373bc` |
| **TransferPolicy** | `0x253c5bf8e47014358e1845305b2e133cc2106e24dce1760a4cb2cedb2e0c8032` |
| **TransferPolicyCap** | `0xf3f42d23f43919b6deb36af6c67bed6c0e4b29a5c9577843021d2d6e59e21b32` |

## Requirements

- **Sui Wallet** browser extension ([Install](https://chrome.google.com/webstore/detail/sui-wallet/opcgpfmipidbgpenhmajoajpbobppdil))
- **Admin Wallet** with TransferPolicyCap ownership
- **Browser** (Chrome, Firefox, or Brave recommended)

## How to Claim Royalties

1. Open the dashboard (deployed on Vercel or locally)
2. Click "Connect Sui Wallet"
3. Select the wallet that owns the TransferPolicyCap
4. The royalty balance will be displayed at the top
5. Click "Claim Royalties" button
6. Approve the transaction in your wallet
7. Wait for confirmation (balance will refresh automatically)

## Dashboard Sections

### 💰 Royalty Rewards
- Shows available royalty balance from secondary sales
- Claim button (only enabled for authorized wallet)
- Transaction status and confirmation

### 📊 Treasury Information
- Treasury wallet address
- Current treasury balance
- Note: Minting fees go directly to treasury (different from royalties)

### 📈 Collection Statistics
- Total Minted
- Premint Minted
- Phase 1/2/3 Minted
- Public Minted
- Remaining NFTs

### 🔗 Contract Information
- Package ID with explorer link
- NFTCollection ID with explorer link

## Technical Details

### Royalties vs Treasury

**Royalties** (what this dashboard claims):
- Come from secondary sales on marketplaces
- Stored in the TransferPolicy balance
- Require TransferPolicyCap to withdraw
- Current balance: ~23.43 SUI

**Treasury** (separate funds):
- Come from primary NFT minting
- Sent directly to treasury address
- Require treasury wallet private key to access
- View-only in this dashboard

### Smart Contract

The Puppets NFT collection uses Sui's standard `TransferPolicy` for royalty enforcement. The `withdraw` function is called to claim accumulated fees:

```move
public fun withdraw<T>(
    policy: &mut TransferPolicy<T>,
    cap: &TransferPolicyCap<T>,
    amount: Option<u64>,
    ctx: &mut TxContext
): Coin<SUI>
```

## Security Notes

- This dashboard only reads public blockchain data
- Transactions require explicit wallet approval
- No private keys are stored or transmitted
- All RPC calls go directly to Sui mainnet
- Open source - review the code before use

## Troubleshooting

### Connect button does nothing / No wallet detected

**Solution:**
1. Install the [Sui Wallet extension](https://chromewebstore.google.com/detail/sui-wallet/opcgpfmipidbgpenhmajoajpbobppdil)
2. Make sure the extension is **enabled** in your browser
3. **Refresh the page** after installing
4. Open browser console (F12) and check for logs
5. Look for `window.suiWallets:` in console - should not be `undefined`

**Still not working?**
- Try a different browser (Chrome, Brave, or Edge)
- Disable other wallet extensions temporarily
- Check console for error messages
- Make sure you're using the latest Sui Wallet version

### "Permission Required" message
- You need to connect with the wallet that owns the TransferPolicyCap
- Check the displayed cap owner address matches your wallet
- The dashboard shows both addresses so you can verify

### Transaction fails
- Ensure you have enough SUI for gas fees (~0.01 SUI)
- Check that you're connected to Sui Mainnet (not Testnet)
- Try refreshing the page and reconnecting
- Check the transaction error in console (F12)

### Balance not updating
- Wait 2-3 seconds after transaction confirmation
- Refresh the page manually if needed
- Check transaction on SuiScan using the provided link

### Wallet connects but shows errors
- Open browser console (F12) and look for red error messages
- Check if you're on the correct network (Mainnet)
- Verify your wallet has some SUI for gas fees
- Try disconnecting and reconnecting the wallet

## Links

- **SuiScan Package**: [View Contract](https://suiscan.xyz/mainnet/object/0xefb46efef2715424b184462c4e3c831456909efe2fbe72b20e4f80e1bd80ce03)
- **TransferPolicy**: [View on SuiScan](https://suiscan.xyz/mainnet/object/0x253c5bf8e47014358e1845305b2e133cc2106e24dce1760a4cb2cedb2e0c8032)
- **Sui Wallet**: [Chrome Extension](https://chrome.google.com/webstore/detail/sui-wallet/opcgpfmipidbgpenhmajoajpbobppdil)
- **Sui Documentation**: [docs.sui.io](https://docs.sui.io)

## License

MIT

## Support

For issues or questions, please open an issue on GitHub.

---

Built with ❤️ for the Puppets NFT community
