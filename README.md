
    it('Handling new Grips', function () {
      cy.visit('https://alapanme.github.io/testing-cypress.html')
    
      cy.window().then((win) => {
        cy.stub(win, 'open', url => {
          win.location.href = 'https://the-internet.herokuapp.com/';
        }).as("popup")
      })
    
      cy.get('button').click()
    
      cy.get('@popup').should("be.called")
    
      // Commands targeting https://the-internet.herokuapp.com go here
      cy.origin('https://the-internet.herokuapp.com', () => {
        cy.get('h1').should('have.text', 'Welcome to the-internet')
        cy.get(':nth-child(1) > a').click()
        cy.wait(10000)
        cy.go('back')
      })
    })

