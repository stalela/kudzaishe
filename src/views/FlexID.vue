<template>
  <div class="article-content">
    <router-link to="/" class="back-link">← Back to Home</router-link>

    <!-- HEADLINE -->
    <h1>Protocol for Insurable Verifiable Credentials</h1>
    <span class="subtitle">System Architecture & Economic Mechanism Design</span>

    <!-- CONTENT START -->
    <p>
      Digital identity systems often fail at the edge cases. Cryptography can prove that a key signed a document, but it cannot prove that the issuer behind the key acted in good faith or that the data is accurate.
    </p>

    <p>
      This project was an architectural attempt to solve the "Bad Data" problem by introducing a financial layer to the trust stack. We treated identity verification not just as a boolean (True/False), but as a risk assessment backed by financial liability.
    </p>

    <h2>The Core Thesis</h2>
    <pre><code><span class="comment">// The "VISA Model" for Identity</span>

<span class="type">IF</span> (Identity_Risk > 0) {

    Apply_Insurance_Wrapper();

}

<span class="comment">// Result: The Verifier trusts the Insurance Policy (Liability), not just the Data.</span></code></pre>

    <p>
      Just as financial instruments are made usable by wrapping them in insurance and guarantees, we made digital identity usable by wrapping credentials in financial liability. If an issuer issues a credential incorrectly, they or their insurer pay out.
    </p>

    <h2>Verifiable Credentials as Risk Mitigation</h2>

    <p>
      Consider a scenario where a user goes to <strong>Bank A</strong> to open an account. They perform KYC (Know Your Customer), liveness checks, and submit documents. Bank A then issues a <strong>KYC Verifiable Credential</strong> to the user's wallet.
    </p>

    <p>
      Later, the user goes to <strong>Bank B</strong> (or a microfinance institution) to get a loan. Instead of redoing the entire KYC process—which is redundant and costly—the user simply presents the KYC credential from Bank A.
    </p>

    <p>
      While cryptographic signatures prove the credential <em>came</em> from Bank A and hasn't been tampered with, they don't prove the data is <em>accurate</em>. How can Bank B be sure Bank A issued that credential in good faith? If the user is actually a fraudster using a misrepresented identity, Bank B faces financial loss.
    </p>

    <h2>The Solution: Insurable Credentials</h2>

    <p>
      To make their credentials widely acceptable, issuers (like Bank A) can attach an <strong>insurance policy</strong> to the credentials they issue.
    </p>

    <p>
      Effectively, Bank A says:
      <em>"I verify this user's identity is accurate. I am so confident in my verification that I am willing to pay you $100 if you incur any financial loss because this information was misrepresented."</em>
    </p>

    <p>
      This transforms a "claim" into an "asset."
    </p>

    <h3>Credential Grading & Automated Acceptance</h3>

    <p>
      This system creates a <strong>rating system</strong> for credentials. Verifiers (or their AI agents) can now set automated policies based on risk appetite:
    </p>

    <ul>
      <li><em>"I only accept credentials insured for at least $500."</em></li>
      <li><em>"I only accept credentials from Grade A issuers with a solvency ratio > 95%."</em></li>
    </ul>

    <p>
      This economic mechanism aligns incentives:
    </p>

    <ul>
      <li><strong>Issuers</strong> are incentivized to perform high-quality verification to avoid payouts.</li>
      <li><strong>Issuers</strong> can earn revenue (a "cut") every time their high-quality credential is used by a relying party.</li>
      <li><strong>Verifiers</strong> reduce their risk and operational costs by relying on insured data.</li>
    </ul>

    <h2>System Architecture</h2>

    <p>
      Most Identity systems use a 3-party model (Issuer, Holder, Verifier). We introduced a 4th node: <strong>The Insurer</strong> (which can be the Issuer themselves or a third-party underwriter).
    </p>

    <div class="architecture-diagram">
      <div class="node">Issuer</div>
      <div class="arrow"><span class="label">Credential + Liability</span></div>
      <div class="node insurer">Insurer</div>
      <div class="arrow"><span class="label">Insured VC</span></div>
      <div class="node">Verifier</div>
    </div>

    <p style="font-size: 13px; color: var(--text-primary); text-align: center; margin-top: -20px;">
      Fig 1. The Value Flow: Turning "Claims" into "Insured Assets"
    </p>

    <h2>The "Market for Trust"</h2>

    <p>
      This architecture creates a marketplace. High-quality issuers (who rarely verify fake docs) get cheaper insurance premiums or can offer higher guarantees. Low-quality issuers get priced out or downgraded.
    </p>

    <p>
      This brings <strong>audit-grade observability</strong> to the messy world of human identity. It hardens the "soft edges" of reality with economic incentives, ensuring that the entity vouching for the data has "skin in the game."
    </p>

    <br>
    <hr style="border: 0; border-top: 1px solid var(--border);">
    <br>

    <p style="font-size: 13px; color: var(--text-primary);">
      <em>Originally published as part of a technical whitepaper on decentralized identity (2021-2023). Co-authored by Kudzaishe Zharare.</em>
    </p>
  </div>
</template>

<script>
export default {
  name: 'FlexID'
}
</script>

<style scoped>
.article-content {
  max-width: 700px;
  margin: 80px auto;
  padding: 24px;
}

.architecture-diagram {
  background: #151515;
  border: 1px solid var(--border);
  padding: 40px;
  margin: 40px 0;
  position: relative;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.node {
  border: 1px solid var(--accent);
  padding: 10px 20px;
  border-radius: 4px;
  font-size: 13px;
  background: rgba(164, 120, 90, 0.1);
}

.node.insurer {
  border-color: #fff;
  color: #fff;
  background: rgba(255,255,255,0.05);
}

.arrow {
  flex: 1;
  height: 1px;
  background: var(--border);
  position: relative;
  margin: 0 10px;
}

.arrow::after {
  content: '>';
  position: absolute;
  right: 0;
  top: -7px;
  color: var(--border);
}

.label {
  position: absolute;
  top: -20px;
  left: 50%;
  transform: translateX(-50%);
  font-size: 11px;
  color: var(--text-secondary);
}
</style>
