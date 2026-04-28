
import React, { useMemo, useState } from 'react';

const PRICING = {
  partialRate: 2.5,
  fullRate: 5.75,
  partialMaxDiscount: 0.5,
  fullMaxDiscount: 1.0,
  dehumidifier: { EO70: 3500, EO100: 3985 },
  frenchDrain: 37,
  sumpPump: 2400,
  crawlspaceSanitation: 1.35,
  spotTreatment: 875,
  crawlDoor: 775,
  insulationRemoval: 1.5,
  debrisLt: 385,
  debrisHvy: 815,
  dumpster: 1590,
  partialAnnual: 250,
  fullAnnual: 299,
  tripCharge: 250,
};

const money = (n) => new Intl.NumberFormat('en-US', { style: 'currency', currency: 'USD', maximumFractionDigits: 0 }).format(Number.isFinite(n) ? n : 0);
const money2 = (n) => new Intl.NumberFormat('en-US', { style: 'currency', currency: 'USD', maximumFractionDigits: 2 }).format(Number.isFinite(n) ? n : 0);
const num = (n) => new Intl.NumberFormat('en-US').format(Number.isFinite(n) ? n : 0);
const toNum = (v) => { const n = Number(v); return Number.isFinite(n) ? n : 0; };

const inputStyle = { width:'100%', height:46, borderRadius:12, border:'1px solid #d1d5db', padding:'0 12px', fontSize:16, boxSizing:'border-box', background:'#fff' };

function Field({ label, children }) {
  return <div><label className="field-label">{label}</label>{children}</div>;
}

function SelectField({ value, setValue, options }) {
  return <select style={inputStyle} value={value} onChange={(e)=>setValue(e.target.value)}>{options.map(x => <option key={x} value={x}>{x}</option>)}</select>;
}

function SummaryRow({ label, value, strong }) {
  return <div className={strong ? 'summary-row strong' : 'summary-row'}><span>{label}</span><b>{value}</b></div>;
}

export default function App() {
  const [customerName, setCustomerName] = useState('');
  const [propertyAddress, setPropertyAddress] = useState('');
  const [salesRep, setSalesRep] = useState('');
  const [repPhone, setRepPhone] = useState('205-362-8343');
  const [quoteDate, setQuoteDate] = useState(new Date().toISOString().slice(0, 10));
  const [quoteType, setQuoteType] = useState('Partial Encap');
  const [sqFt, setSqFt] = useState('');
  const [discount, setDiscount] = useState('');
  const [frenchDrainQty, setFrenchDrainQty] = useState('');
  const [sumpPump, setSumpPump] = useState('No');
  const [crawlspaceSanitationQty, setCrawlspaceSanitationQty] = useState('');
  const [spotTreatment, setSpotTreatment] = useState('No');
  const [crawlDoorQty, setCrawlDoorQty] = useState('');
  const [insulationRemovalQty, setInsulationRemovalQty] = useState('');
  const [debrisRemoval, setDebrisRemoval] = useState('None');
  const [dumpster, setDumpster] = useState('No');
  const [maintenance, setMaintenance] = useState('None');
  const [tripCharge, setTripCharge] = useState('No');
  const [notes, setNotes] = useState('');

  const calc = useMemo(() => {
    const sf = toNum(sqFt);
    const baseRate = quoteType === 'Full Encap' ? PRICING.fullRate : PRICING.partialRate;
    const maxDiscount = quoteType === 'Full Encap' ? PRICING.fullMaxDiscount : PRICING.partialMaxDiscount;
    const enteredDiscount = toNum(discount);
    const appliedDiscount = Math.min(enteredDiscount, maxDiscount);
    const finalRate = Math.max(baseRate - appliedDiscount, 0);
    const coreQuote = sf * finalRate;
    const dehumidifier = quoteType === 'Full Encap' ? (sf < 2100 ? 'EO70' : 'EO100') : 'None';
    const dehumidifierTotal = dehumidifier === 'None' ? 0 : PRICING.dehumidifier[dehumidifier];
    const frenchDrainTotal = toNum(frenchDrainQty) * PRICING.frenchDrain;
    const sumpPumpTotal = sumpPump === 'Yes' ? PRICING.sumpPump : 0;
    const sanitationTotal = toNum(crawlspaceSanitationQty) * PRICING.crawlspaceSanitation;
    const spotTotal = spotTreatment === 'Yes' ? PRICING.spotTreatment : 0;
    const doorTotal = toNum(crawlDoorQty) * PRICING.crawlDoor;
    const insulationTotal = toNum(insulationRemovalQty) * PRICING.insulationRemoval;
    const debrisTotal = debrisRemoval === 'LT' ? PRICING.debrisLt : debrisRemoval === 'HVY' ? PRICING.debrisHvy : 0;
    const dumpsterTotal = dumpster === 'Yes' ? PRICING.dumpster : 0;
    const maintTotal = maintenance === 'Partial Annual' ? PRICING.partialAnnual : maintenance === 'Full Annual' ? PRICING.fullAnnual : 0;
    const tripTotal = tripCharge === 'Yes' ? PRICING.tripCharge : 0;
    const addOnsTotal = dehumidifierTotal + frenchDrainTotal + sumpPumpTotal + sanitationTotal + spotTotal + doorTotal + insulationTotal + debrisTotal + dumpsterTotal + maintTotal + tripTotal;
    const grandTotal = coreQuote + addOnsTotal;
    const projectLines = [
      { service: `${quoteType} (${num(sf)} sq ft @ ${money2(finalRate)}/sq ft)`, amount: coreQuote },
      { service: dehumidifier !== 'None' ? `Aprilaire Dehumidifier ${dehumidifier} (Installed)` : '', amount: dehumidifierTotal },
      { service: toNum(frenchDrainQty) > 0 ? `French Drain (${num(toNum(frenchDrainQty))} linear ft)` : '', amount: frenchDrainTotal },
      { service: sumpPump === 'Yes' ? 'Sump Pump (includes Electric)' : '', amount: sumpPumpTotal },
      { service: toNum(crawlspaceSanitationQty) > 0 ? `Crawlspace Sanitation (${num(toNum(crawlspaceSanitationQty))} sq ft)` : '', amount: sanitationTotal },
      { service: spotTreatment === 'Yes' ? 'Spot Treatment' : '', amount: spotTotal },
      { service: toNum(crawlDoorQty) > 0 ? `Crawl Space Door Installation (${num(toNum(crawlDoorQty))})` : '', amount: doorTotal },
      { service: toNum(insulationRemovalQty) > 0 ? `Insulation Removal (${num(toNum(insulationRemovalQty))} sq ft)` : '', amount: insulationTotal },
      { service: debrisRemoval !== 'None' ? `${debrisRemoval === 'LT' ? 'Light' : 'Heavy'} Clean-Out` : '', amount: debrisTotal },
      { service: dumpster === 'Yes' ? 'Dumpster' : '', amount: dumpsterTotal },
      { service: maintenance !== 'None' ? `Maintenance / Inspection - ${maintenance}` : '', amount: maintTotal },
      { service: tripCharge === 'Yes' ? 'Trip Charge' : '', amount: tripTotal },
    ].filter(x => x.service && x.amount > 0);
    const warnings = [];
    if (enteredDiscount > maxDiscount) warnings.push(`Discount capped at ${money2(maxDiscount)} per sq ft.`);
    if (quoteType === 'Full Encap') warnings.push(`Full Encap auto-selected ${dehumidifier}.`);
    if (toNum(frenchDrainQty) > 0 && sumpPump === 'No') warnings.push('Consider adding a sump pump when quoting French Drain.');
    return { sf, baseRate, maxDiscount, appliedDiscount, finalRate, coreQuote, dehumidifier, addOnsTotal, grandTotal, projectLines, warnings };
  }, [quoteType, sqFt, discount, frenchDrainQty, sumpPump, crawlspaceSanitationQty, spotTreatment, crawlDoorQty, insulationRemovalQty, debrisRemoval, dumpster, maintenance, tripCharge]);

  const resetForm = () => {
    setCustomerName(''); setPropertyAddress(''); setSalesRep(''); setQuoteDate(new Date().toISOString().slice(0, 10));
    setQuoteType('Partial Encap'); setSqFt(''); setDiscount(''); setFrenchDrainQty(''); setSumpPump('No');
    setCrawlspaceSanitationQty(''); setSpotTreatment('No'); setCrawlDoorQty(''); setInsulationRemovalQty('');
    setDebrisRemoval('None'); setDumpster('No'); setMaintenance('None'); setTripCharge('No'); setNotes('');
  };

  const numberInput = (value, setter, step='1') => <input style={inputStyle} type="number" min="0" step={step} value={value} onChange={(e)=>setter(e.target.value)} />;

  return (
    <div className="app">
      <div className="no-print topbar">
        <div><h1>Envirospace Quote App</h1><p>Waynes-style proposal template • Wildlife section removed</p></div>
        <div className="top-actions">
          <span className="pill">Rate {money2(calc.finalRate)}/sq ft</span>
          <span className="pill total">{money(calc.grandTotal)}</span>
          <button onClick={() => window.print()}>Print Proposal</button>
          <button className="secondary" onClick={resetForm}>New Quote</button>
        </div>
      </div>

      <div className="workspace no-print">
        <section className="card">
          <h2>Customer & Job Info</h2>
          <div className="grid two">
            <Field label="Customer Name"><input style={inputStyle} value={customerName} onChange={(e)=>setCustomerName(e.target.value)} /></Field>
            <Field label="Property Address"><input style={inputStyle} value={propertyAddress} onChange={(e)=>setPropertyAddress(e.target.value)} /></Field>
            <Field label="Sales Rep"><input style={inputStyle} value={salesRep} onChange={(e)=>setSalesRep(e.target.value)} /></Field>
            <Field label="Rep Phone"><input style={inputStyle} value={repPhone} onChange={(e)=>setRepPhone(e.target.value)} /></Field>
            <Field label="Quote Date"><input style={inputStyle} type="date" value={quoteDate} onChange={(e)=>setQuoteDate(e.target.value)} /></Field>
          </div>

          <h2>Core Pricing</h2>
          <div className="grid four">
            <Field label="Quote Type"><SelectField value={quoteType} setValue={setQuoteType} options={['Partial Encap','Full Encap']} /></Field>
            <Field label="Crawlspace Sq Ft">{numberInput(sqFt, setSqFt)}</Field>
            <Field label="Discount / Sq Ft">{numberInput(discount, setDiscount, '0.01')}</Field>
            <Field label="Auto Dehumidifier"><input style={{...inputStyle, background:'#f4f7f4', fontWeight:700}} readOnly value={calc.dehumidifier} /></Field>
          </div>

          <h2>Add-Ons & Remediation</h2>
          <div className="grid three">
            <Field label="French Drain (Linear Ft)">{numberInput(frenchDrainQty, setFrenchDrainQty)}</Field>
            <Field label="Sump Pump"><SelectField value={sumpPump} setValue={setSumpPump} options={['No','Yes']} /></Field>
            <Field label="Crawlspace Sanitation (Sq Ft)">{numberInput(crawlspaceSanitationQty, setCrawlspaceSanitationQty, '0.01')}</Field>
            <Field label="Spot Treatment"><SelectField value={spotTreatment} setValue={setSpotTreatment} options={['No','Yes']} /></Field>
            <Field label="Crawl Door Qty">{numberInput(crawlDoorQty, setCrawlDoorQty)}</Field>
            <Field label="Insulation Removal (Sq Ft)">{numberInput(insulationRemovalQty, setInsulationRemovalQty, '0.01')}</Field>
            <Field label="Debris Removal"><SelectField value={debrisRemoval} setValue={setDebrisRemoval} options={['None','LT','HVY']} /></Field>
            <Field label="Dumpster"><SelectField value={dumpster} setValue={setDumpster} options={['No','Yes']} /></Field>
            <Field label="Maintenance / Inspection"><SelectField value={maintenance} setValue={setMaintenance} options={['None','Partial Annual','Full Annual']} /></Field>
            <Field label="Trip Charge"><SelectField value={tripCharge} setValue={setTripCharge} options={['No','Yes']} /></Field>
          </div>

          <h2>Proposal Notes</h2>
          <textarea style={{...inputStyle, height:110, paddingTop:12}} value={notes} onChange={(e)=>setNotes(e.target.value)} />
        </section>

        <aside className="card summary">
          <h2>Quote Summary</h2>
          <SummaryRow label="Base Rate / Sq Ft" value={money2(calc.baseRate)} />
          <SummaryRow label="Max Allowed Discount" value={money2(calc.maxDiscount)} />
          <SummaryRow label="Applied Discount" value={money2(calc.appliedDiscount)} />
          <SummaryRow label="Final Rate / Sq Ft" value={money2(calc.finalRate)} strong />
          <SummaryRow label="Core Quote" value={money(calc.coreQuote)} />
          <SummaryRow label="Add-Ons Total" value={money(calc.addOnsTotal)} />
          <SummaryRow label="TOTAL INVESTMENT" value={money(calc.grandTotal)} strong />
          {calc.warnings.length > 0 && <div className="warnings">{calc.warnings.map(w => <div key={w}>{w}</div>)}</div>}
        </aside>
      </div>

      <Proposal customerName={customerName} propertyAddress={propertyAddress} salesRep={salesRep} repPhone={repPhone} quoteDate={quoteDate} quoteType={quoteType} notes={notes} calc={calc} />
    </div>
  );
}

function Proposal({ customerName, propertyAddress, salesRep, repPhone, quoteType, notes, calc }) {
  return (
    <div className="proposal-page">
      <header className="proposal-header">
        <div className="brand-seal">W</div>
        <div className="brand-main"><div className="brand-name">WAYNES</div><div className="brand-sub">PEST CONTROL</div><div className="brand-line">PEST • TERMITE • WILDLIFE</div></div>
        <div className="proposal-title"><h1>CRAWL SPACE<br/>ENCAPSULATION QUOTE</h1><p>Protecting your home from the ground up.</p></div>
      </header>
      <div className="proposal-divider"></div>

      <main className="proposal-grid">
        <section className="proposal-card main-scope">
          <div className="proposal-card-title">{quoteType === 'Full Encap' ? 'FULL CRAWL SPACE ENCAPSULATION SYSTEM' : 'PARTIAL CRAWL SPACE ENCAPSULATION SYSTEM'}</div>
          <div className="proposal-card-body">
            <p className="intro">Our encapsulation system is designed to control moisture, improve air quality, and protect the structural integrity of your home for years to come.</p>
            <ul className="check-list">
              <li>Full crawl space sealing system</li>
              <li>Installation of heavy-duty vapor barrier on floors and walls</li>
              <li>Sealing of vents and entry points</li>
              <li>Professional-grade dehumidifier installation when applicable</li>
              <li>Moisture control to reduce humidity, mold risk, and wood rot</li>
              <li>Improves energy efficiency and overall air quality in the home</li>
            </ul>
            <div className="breakdown">
              <div className="breakdown-title">PROJECT BREAKDOWN</div>
              <table><thead><tr><th>SERVICE</th><th>INVESTMENT</th></tr></thead><tbody>
                {calc.projectLines.length ? calc.projectLines.map((line, idx) => <tr key={idx}><td>{line.service}</td><td>{money(line.amount)}</td></tr>) : <tr><td>Enter quote details to generate project breakdown</td><td>{money(0)}</td></tr>}
              </tbody></table>
              <div className="total-bar"><div>TOTAL INVESTMENT</div><strong>{money(calc.grandTotal)}</strong></div>
            </div>
          </div>
        </section>

        <section className="proposal-card services">
          <div className="proposal-card-title">ADDITIONAL SERVICES</div>
          <div className="proposal-card-body">
            <div className="service-feature">
              <div className="icon-circle">💧</div>
              <h2>CRAWL SPACE<br/>SANITATION</h2><h3>(RECOMMENDED)</h3>
              <ul><li>Apply antimicrobial treatment</li><li>Helps prevent mold and mildew</li><li>Addresses musty odors at the source</li><li>Promotes a cleaner, healthier crawl space environment</li></ul>
              <div className="investment">INVESTMENT: {money(PRICING.crawlspaceSanitation * (calc.sf || 0))}</div>
            </div>
            <div className="service-feature lower">
              <div className="icon-circle">🛡</div><h2>MOISTURE<br/>PROTECTION</h2><h3>(RECOMMENDED)</h3>
              <ul><li>Protects structural integrity</li><li>Improves indoor air quality</li><li>Reduces risk of pest pressure</li></ul>
            </div>
          </div>
        </section>
      </main>

      <section className="difference">
        <div className="difference-title">THE WAYNES DIFFERENCE</div>
        <div className="difference-items">
          <div><div className="diff-icon">💧</div><b>ELIMINATES<br/>MOISTURE</b><span>Issues at the source</span></div>
          <div><div className="diff-icon">🛡</div><b>PROTECTS<br/>STRUCTURAL INTEGRITY</b><span>of your home</span></div>
          <div><div className="diff-icon">〰</div><b>IMPROVES<br/>AIR QUALITY</b><span>throughout your home</span></div>
          <div><div className="diff-icon">🚫</div><b>PREVENTS<br/>PEST PROBLEMS</b><span>now and in the future</span></div>
          <div><div className="diff-icon">⌂</div><b>INCREASES<br/>HOME EFFICIENCY & VALUE</b></div>
        </div>
      </section>

      <section className="proposal-footer-info">
        <div><div className="footer-icon">📅</div><b>NEXT STEPS</b><p>Scheduling is first-come, first-served. Contact us today to secure your spot on our schedule.</p></div>
        <div><div className="footer-icon">☎</div><b>QUESTIONS?</b><p>We’re here to help. Call or text anytime—we’re happy to walk you through everything.</p></div>
        <div><em>Thank you,</em><div className="signature-line"></div><b>{salesRep || 'RYAN'}</b><p>Waynes Pest Control</p><p>{customerName ? `Prepared for: ${customerName}` : ''}</p><p>{propertyAddress || ''}</p>{notes ? <p className="notes">{notes}</p> : null}</div>
      </section>

      <footer className="proposal-footer"><span>☎ {repPhone || '205-362-8343'}</span><span>callwaynes.com</span><span>INTEGRITY. CHARACTER. COURAGE. PERSEVERANCE.</span></footer>
    </div>
  );
}
