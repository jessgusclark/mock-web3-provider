# mock-web3-provider

A mock web3 provider for Cypress built in Cyprus.

Under development and missing many request methods and listeners. See below under 'contributing' to help!

## Usage

Setup the mock provider before the window loads and set it to the `win.ethereum` variable. For a complete integration example, see the [rLogin basic dapp test integration](https://github.com/rsksmart/rlogin-sample-apps/blob/main/basic-dapp/cypress/integration/injected_spec.js).

```
import mockProvider from 'mock-web3-provider'

describe('test interaction with web3', () => {
  beforeEach(() => {
    cy.on("window:before:load", (win) => {
      win.ethereum = mockProvider({ address, privateKey, chainId: 31, debug:false })

      // when used with rLogin:
      cy.visit('/')
      cy.contains('Connect with rLogin').click()
      cy.contains('MetaMask').click()
    })
  })

  // assuming there is an item displaying the account when the user logs in
  it('displays the account', () => {
    cy.get('.account').should('have.text', `Account: ${address}`)
  })

  // additional e2e tests...
})
```
## Contributing

Additional mock methods should be added as well as the event listeners. PRs are welcomed as long as corresponding tests are included.
