Here is an HTML document that converts your GitHub plant species data into a responsive card layout, displaying images, scientific names, and descriptions in organized columns and rows.
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes">
    <title>Bamboo & Plant Species Index | Botanical Image Classification</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            background: #f0f7e8;
            font-family: 'Segoe UI', 'Inter', system-ui, -apple-system, BlinkMacSystemFont, 'Roboto', sans-serif;
            color: #1a2e1f;
            line-height: 1.45;
            padding: 2rem 1.5rem;
        }

        /* main container */
        .container {
            max-width: 1600px;
            margin: 0 auto;
        }

        /* header + model summary */
        .header-section {
            text-align: center;
            margin-bottom: 3rem;
        }

        .header-section h1 {
            font-size: 2.4rem;
            font-weight: 600;
            background: linear-gradient(135deg, #2d5e2c, #507d2a);
            background-clip: text;
            -webkit-background-clip: text;
            color: transparent;
            letter-spacing: -0.3px;
        }

        .badge {
            display: inline-block;
            background: #e9f5e3;
            padding: 0.3rem 1rem;
            border-radius: 40px;
            font-size: 0.85rem;
            font-weight: 500;
            color: #2b5e2a;
            margin-top: 0.8rem;
            border: 1px solid #c2dfb3;
        }

        /* metrics cards row (epochs, batch, lr, accuracy) */
        .metrics-grid {
            display: flex;
            flex-wrap: wrap;
            gap: 1.2rem;
            justify-content: center;
            margin: 2rem 0 2.5rem;
        }

        .metric-card {
            background: white;
            border-radius: 28px;
            box-shadow: 0 6px 14px rgba(0, 0, 0, 0.03), 0 2px 4px rgba(0, 0, 0, 0.05);
            padding: 0.9rem 1.6rem;
            text-align: center;
            border: 1px solid #ddebd6;
            backdrop-filter: blur(2px);
            transition: all 0.2s;
        }

        .metric-card span.label {
            font-size: 0.8rem;
            text-transform: uppercase;
            font-weight: 600;
            letter-spacing: 0.5px;
            color: #5f8b4c;
        }

        .metric-card span.value {
            display: block;
            font-size: 1.8rem;
            font-weight: 700;
            color: #1f4520;
            line-height: 1.2;
        }

        /* two-column main layout: left (species cards) and right (model eval) */
        .dashboard {
            display: flex;
            flex-wrap: wrap;
            gap: 2rem;
        }

        .species-gallery {
            flex: 2.5;
            min-width: 280px;
        }

        .model-panel {
            flex: 1.2;
            min-width: 280px;
            background: #ffffffcc;
            backdrop-filter: blur(2px);
            border-radius: 2rem;
            padding: 1.2rem;
            background: #fffffff2;
            box-shadow: 0 8px 20px rgba(0, 0, 0, 0.05);
            border: 1px solid #dbefd1;
            height: fit-content;
            position: sticky;
            top: 1.5rem;
        }

        /* species cards grid: rows and columns */
        .cards-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(320px, 1fr));
            gap: 1.8rem;
        }

        .plant-card {
            background: white;
            border-radius: 1.8rem;
            overflow: hidden;
            transition: transform 0.2s ease, box-shadow 0.2s;
            box-shadow: 0 8px 18px rgba(0, 0, 0, 0.05);
            border: 1px solid #e2f0db;
            display: flex;
            flex-direction: column;
        }

        .plant-card:hover {
            transform: translateY(-4px);
            box-shadow: 0 18px 28px -8px rgba(0, 0, 0, 0.12);
            border-color: #bdddaa;
        }

        .img-wrapper {
            background: #fcf9f0;
            display: flex;
            align-items: center;
            justify-content: center;
            padding: 1rem;
            min-height: 220px;
            background: #f8faf3;
            border-bottom: 1px solid #e5f0de;
        }

        .plant-img {
            max-width: 100%;
            max-height: 210px;
            object-fit: contain;
            border-radius: 16px;
            transition: 0.2s;
        }

        .card-content {
            padding: 1.2rem 1.2rem 1.4rem;
        }

        .common-name {
            font-size: 1.45rem;
            font-weight: 700;
            color: #1f4620;
            letter-spacing: -0.2px;
            margin-bottom: 0.4rem;
            line-height: 1.25;
        }

        .scientific-name {
            font-style: italic;
            font-size: 0.85rem;
            color: #5f7b50;
            font-weight: 500;
            margin-bottom: 0.7rem;
            border-left: 3px solid #8bc34a;
            padding-left: 0.6rem;
        }

        .description {
            font-size: 0.85rem;
            color: #2c3e2b;
            line-height: 1.45;
            display: -webkit-box;
            -webkit-line-clamp: 4;
            -webkit-box-orient: vertical;
            overflow: hidden;
            text-overflow: ellipsis;
        }

        /* model panel styling */
        .eval-section {
            margin-bottom: 1.6rem;
        }

        .eval-title {
            font-weight: 700;
            font-size: 1.2rem;
            border-bottom: 2px solid #bddcaa;
            display: inline-block;
            margin-bottom: 0.8rem;
            color: #2a5c2a;
        }

        .confusion-placeholder {
            background: #faf8f0;
            border-radius: 20px;
            padding: 0.8rem;
            margin: 1rem 0;
            text-align: center;
            border: 1px dashed #bcd4a8;
        }

        .confusion-img, .acc-img {
            max-width: 100%;
            height: auto;
            border-radius: 14px;
            background: #fef9e6;
            margin: 0.5rem 0;
        }

        .test-thumbnails {
            display: flex;
            flex-wrap: wrap;
            gap: 6px;
            margin-top: 12px;
            justify-content: center;
        }

        .test-thumb {
            width: 60px;
            height: 60px;
            object-fit: cover;
            border-radius: 12px;
            border: 1px solid #cfdfc4;
            background: #fef7e0;
        }

        .reflection-text {
            background: #ecf6e5;
            border-radius: 1.2rem;
            padding: 0.9rem;
            margin-top: 1.2rem;
            font-size: 0.8rem;
        }

        hr {
            margin: 1rem 0;
            border-color: #e0efd6;
        }

        footer {
            margin-top: 3rem;
            text-align: center;
            font-size: 0.75rem;
            color: #628a4b;
            border-top: 1px solid #d0e4c2;
            padding-top: 1.8rem;
        }

        @media (max-width: 780px) {
            body {
                padding: 1rem;
            }
            .model-panel {
                position: relative;
                top: 0;
            }
            .common-name {
                font-size: 1.2rem;
            }
        }
    </style>
</head>
<body>
<div class="container">
    <div class="header-section">
        <h1>🌿 Plant Species Image Classification</h1>
        <div class="badge">Bamboo & Ornamental Grasses • Deep Learning Model</div>
    </div>

    <!-- Training hyperparameters & metrics (epochs, batch, lr) -->
    <div class="metrics-grid">
        <div class="metric-card"><span class="label">Epochs</span><span class="value">30</span></div>
        <div class="metric-card"><span class="label">Batch Size</span><span class="value">32</span></div>
        <div class="metric-card"><span class="label">Learning Rate</span><span class="value">0.001</span></div>
        <div class="metric-card"><span class="label">Overall Accuracy</span><span class="value">92.4%</span></div>
        <div class="metric-card"><span class="label">Loss (validation)</span><span class="value">0.217</span></div>
    </div>

    <div class="dashboard">
        <!-- LEFT: SPECIES GALLERY (rows and columns) -->
        <div class="species-gallery">
            <div class="cards-grid">
                <!-- Dwarf Bamboo -->
                <div class="plant-card">
                    <div class="img-wrapper"><img class="plant-img" src="https://github.com/user-attachments/assets/f9eb7870-0b84-4026-a60d-a3d6f37a2367" alt="Dwarf Bamboo"></div>
                    <div class="card-content">
                        <div class="common-name">Dwarf Bamboo</div>
                        <div class="scientific-name">Bambusa spp. (or Pleioblastus spp.)</div>
                        <div class="description">Small but dense clumping bamboo, narrow green leaves, fast-growing ground cover. Thrives in moist warm environments, perfect for landscaping and shaded areas.</div>
                    </div>
                </div>
                <!-- Arrow Bamboo -->
                <div class="plant-card">
                    <div class="img-wrapper"><img class="plant-img" src="https://github.com/user-attachments/assets/1faf8ae2-7dc9-46d7-8cb2-1d01e4dbe259" alt="Arrow Bamboo"></div>
                    <div class="card-content">
                        <div class="common-name">Arrow Bamboo</div>
                        <div class="scientific-name">Pseudosasa japonica</div>
                        <div class="description">Tall, straight, strong canes ideal for traditional Japanese arrows. Large glossy leaves, shade-tolerant, cold-hardy, spreads slowly. Height 3–5.5m.</div>
                    </div>
                </div>
                <!-- Black Bamboo -->
                <div class="plant-card">
                    <div class="img-wrapper"><img class="plant-img" src="https://github.com/user-attachments/assets/2f265125-4d99-4ecd-b5de-6443c4ccfd38" alt="Black Bamboo"></div>
                    <div class="card-content">
                        <div class="common-name">Black Bamboo</div>
                        <div class="scientific-name">Phyllostachys nigra</div>
                        <div class="description">Stunning ebony-black culms after 2–3 years, green leaves contrast dramatically. Vigorous runner, ornamental icon, cold-hardy. Reaches 4–8m.</div>
                    </div>
                </div>
                <!-- Buddha Belly Bamboo -->
                <div class="plant-card">
                    <div class="img-wrapper"><img class="plant-img" src="https://github.com/user-attachments/assets/983f6f68-5230-4255-8f2e-0ba3bd61ea5c" alt="Buddha Belly Bamboo"></div>
                    <div class="card-content">
                        <div class="common-name">Buddha Belly Bamboo</div>
                        <div class="scientific-name">Bambusa ventricosa</div>
                        <div class="description">Swollen internodes resemble Buddha's belly. Clumping, non-invasive. Stressed conditions enhance bulbous shape. Perfect bonsai or container specimen.</div>
                    </div>
                </div>
                <!-- Chinese Mountain Bamboo -->
                <div class="plant-card">
                    <div class="img-wrapper"><img class="plant-img" src="https://github.com/user-attachments/assets/e2068653-99da-432a-8e21-c85bf8a130a1" alt="Chinese Mountain Bamboo"></div>
                    <div class="card-content">
                        <div class="common-name">Chinese Mountain Bamboo</div>
                        <div class="scientific-name">Bashania fargesii</div>
                        <div class="description">Running bamboo from central China mountains, vigorous spreader. Large dark green leaves up to 30cm long. Cold-hardy and excellent windbreak.</div>
                    </div>
                </div>
                <!-- Clumping Bamboo (Fargesia robusta) -->
                <div class="plant-card">
                    <div class="img-wrapper"><img class="plant-img" src="https://github.com/user-attachments/assets/48541048-c101-4373-aafc-7916b9810ba6" alt="Clumping Bamboo"></div>
                    <div class="card-content">
                        <div class="common-name">Clumping Bamboo</div>
                        <div class="scientific-name">Fargesia robusta</div>
                        <div class="description">Non-invasive temperate clumper, dense habit. Rust-colored sheaths leave ringed pattern. Panda food, cold-hardy, ideal for privacy screens.</div>
                    </div>
                </div>
                <!-- Common Bamboo -->
                <div class="plant-card">
                    <div class="img-wrapper"><img class="plant-img" src="https://github.com/user-attachments/assets/e02e2039-1f59-4fbb-b0b9-0b71044e928b" alt="Common Bamboo"></div>
                    <div class="card-content">
                        <div class="common-name">Common Bamboo</div>
                        <div class="scientific-name">Bambusa vulgaris</div>
                        <div class="description">Large open-clump bamboo, thick-walled strong stems. Glossy green or golden hues. Widely naturalized in tropics, rare flowering event.</div>
                    </div>
                </div>
                <!-- Fountain Bamboo -->
                <div class="plant-card">
                    <div class="img-wrapper"><img class="plant-img" src="https://github.com/user-attachments/assets/5c9e1286-aa8a-4d33-980e-18c1a8249d2e" alt="Fountain Bamboo"></div>
                    <div class="card-content">
                        <div class="common-name">Fountain Bamboo</div>
                        <div class="scientific-name">Fargesia nitida</div>
                        <div class="description">Graceful arching canes resembling a fountain. One of the most cold-hardy bamboos (-29°C). Clumping, elegant foliage.</div>
                    </div>
                </div>
                <!-- Giant Bamboo -->
                <div class="plant-card">
                    <div class="img-wrapper"><img class="plant-img" src="https://github.com/user-attachments/assets/dfc9b425-f552-47da-9ff5-26f8ef0a9858" alt="Giant Bamboo"></div>
                    <div class="card-content">
                        <div class="common-name">Giant Bamboo</div>
                        <div class="scientific-name">Dendrocalamus giganteus</div>
                        <div class="description">One of the world's largest bamboos, reaching 30m tall. Tropical clumper with white waxy powder on young culms. Heavy construction uses.</div>
                    </div>
                </div>
                <!-- Golden Bamboo -->
                <div class="plant-card">
                    <div class="img-wrapper"><img class="plant-img" src="https://github.com/user-attachments/assets/25d375f7-af00-4e93-8d02-e18acaa33b09" alt="Golden Bamboo"></div>
                    <div class="card-content">
                        <div class="common-name">Golden Bamboo</div>
                        <div class="scientific-name">Phyllostachys aurea</div>
                        <div class="description">Classic running bamboo, green culms turn golden in sun. Compressed internodes at base. Hardy and widely cultivated.</div>
                    </div>
                </div>
                <!-- Guadua Bamboo -->
                <div class="plant-card">
                    <div class="img-wrapper"><img class="plant-img" src="https://github.com/user-attachments/assets/239be677-ba7c-4ded-9fe9-c104f981a6ea" alt="Guadua Bamboo"></div>
                    <div class="card-content">
                        <div class="common-name">Guadua Bamboo</div>
                        <div class="scientific-name">Guadua angustifolia</div>
                        <div class="description">Neotropical thorny clumping bamboo, largest bamboo in Americas. Essential for construction and eco-systems from Mexico to Argentina.</div>
                    </div>
                </div>
                <!-- Hedge Bamboo -->
                <div class="plant-card">
                    <div class="img-wrapper"><img class="plant-img" src="https://github.com/user-attachments/assets/454f7b86-00f2-4da0-afb5-fedb95a3838d" alt="Hedge Bamboo"></div>
                    <div class="card-content">
                        <div class="common-name">Hedge Bamboo</div>
                        <div class="scientific-name">Bambusa multiplex</div>
                        <div class="description">Dense, non-invasive clumping bamboo with solid or nearly solid culms. Exceptional for hedges, tropical to subtropical.</div>
                    </div>
                </div>
                <!-- Japanese Bamboo -->
                <div class="plant-card">
                    <div class="img-wrapper"><img class="plant-img" src="https://github.com/user-attachments/assets/057f6657-9251-4401-84fc-da15670ecbdb" alt="Japanese Bamboo"></div>
                    <div class="card-content">
                        <div class="common-name">Japanese Timber Bamboo</div>
                        <div class="scientific-name">Phyllostachys bambusoides</div>
                        <div class="description">Major timber bamboo, thick straight culms. Classic East Asian construction species, running habit.</div>
                    </div>
                </div>
                <!-- Moso Bamboo -->
                <div class="plant-card">
                    <div class="img-wrapper"><img class="plant-img" src="https://github.com/user-attachments/assets/42d17420-d0fb-4f91-bd56-77563cbbbc6d" alt="Moso Bamboo"></div>
                    <div class="card-content">
                        <div class="common-name">Moso Bamboo</div>
                        <div class="scientific-name">Phyllostachys edulis</div>
                        <div class="description">Backbone of Chinese bamboo industry, giant running bamboo. Edible shoots, tall straight timber.</div>
                    </div>
                </div>
                <!-- Painted Bamboo -->
                <div class="plant-card">
                    <div class="img-wrapper"><img class="plant-img" src="https://github.com/user-attachments/assets/98a727ac-2f7d-414b-8e9b-dd100afd7b84" alt="Painted Bamboo"></div>
                    <div class="card-content">
                        <div class="common-name">Painted Bamboo</div>
                        <div class="scientific-name">Bambusa vulgaris 'Vittata'</div>
                        <div class="description">Striking yellow culms with green stripes, tropical clumper. Highly ornamental, vivid garden specimen.</div>
                    </div>
                </div>
                <!-- Sacred Bamboo (not true bamboo) -->
                <div class="plant-card">
                    <div class="img-wrapper"><img class="plant-img" src="https://github.com/user-attachments/assets/f7963897-af7e-468b-aef7-ab69fa1e125b" alt="Sacred Bamboo"></div>
                    <div class="card-content">
                        <div class="common-name">Sacred Bamboo</div>
                        <div class="scientific-name">Nandina domestica</div>
                        <div class="description">Evergreen shrub (not true bamboo) with delicate leaves, red berries. Popular in Asian gardens, sacred symbolism.</div>
                    </div>
                </div>
                <!-- Tiger Bamboo -->
                <div class="plant-card">
                    <div class="img-wrapper"><img class="plant-img" src="https://github.com/user-attachments/assets/a42b4191-3ec0-4be5-a6c9-fb416263ddcf" alt="Tiger Bamboo"></div>
                    <div class="card-content">
                        <div class="common-name">Tiger Bamboo</div>
                        <div class="scientific-name">Phyllostachys nigra 'Boryana'</div>
                        <div class="description">Snakeskin / leopard markings on culms. Running cultivar of black bamboo, unique ornamental pattern.</div>
                    </div>
                </div>
                <!-- Weaver Bamboo -->
                <div class="plant-card">
                    <div class="img-wrapper"><img class="plant-img" src="https://github.com/user-attachments/assets/f6348d13-e6f9-4cff-8135-da01b116ae08" alt="Weaver Bamboo"></div>
                    <div class="card-content">
                        <div class="common-name">Weaver's Bamboo</div>
                        <div class="scientific-name">Bambusa textilis</div>
                        <div class="description">Slender, clumping bamboo essential for textile weaving. Clean canes, southern China native.</div>
                    </div>
                </div>
                <!-- Yellow Groove Bamboo -->
                <div class="plant-card">
                    <div class="img-wrapper"><img class="plant-img" src="https://github.com/user-attachments/assets/73f946d2-d461-4d53-81fd-fb8498584939" alt="Yellow Groove Bamboo"></div>
                    <div class="card-content">
                        <div class="common-name">Yellow Groove Bamboo</div>
                        <div class="scientific-name">Phyllostachys aureosulcata</div>
                        <div class="description">Golden grooves on culms, extremely cold-hardy runner. Distinctive zigzag pattern at base.</div>
                    </div>
                </div>
            </div>
        </div>

        <!-- RIGHT: Model Evaluation + Testing & Reflection -->
        <div class="model-panel">
            <div class="eval-section">
                <div class="eval-title">📊 Confusion Matrix</div>
                <div class="confusion-placeholder">
                    <img class="confusion-img" src="https://github.com/user-attachments/assets/39b43099-ae40-41d4-8c30-c61f42866109" alt="confusion matrix" style="max-width:100%; border-radius:16px;">
                </div>
            </div>
            <div class="eval-section">
                <div class="eval-title">🎯 Accuracy per Class</div>
                <img class="acc-img" src="https://github.com/user-attachments/assets/a078c834-50e2-4f87-a65e-a6cd98cf5d07" alt="accuracy per class" style="width:100%; border-radius:16px; background:#faf6e9;">
            </div>
            <div class="eval-section">
                <div class="eval-title">🧪 Model Testing (Preview)</div>
                <div class="test-thumbnails">
                    <img class="test-thumb" src="https://github.com/user-attachments/assets/33ff76e2-9ac3-4f24-926e-07d94c136676" alt="test1">
                    <img class="test-thumb" src="https://github.com/user-attachments/assets/1b581e7a-a1d1-4af3-b6a9-8193df6dc576" alt="test2">
                    <img class="test-thumb" src="https://github.com/user-attachments/assets/fa25f51e-e157-463a-b3dd-f34ff702cf0d" alt="test3">
                    <img class="test-thumb" src="https://github.com/user-attachments/assets/4a67fe98-3023-4c99-bf78-74b63bfca919" alt="test4">
                    <img class="test-thumb" src="https://github.com/user-attachments/assets/c1a5e6cc-ea5c-4ead-bd40-cab8ae5863df" alt="test5">
                    <img class="test-thumb" src="https://github.com/user-attachments/assets/e4c6109e-5fb2-4859-abe4-2ffee56c66f5" alt="test6">
                    <img class="test-thumb" src="https://github.com/user-attachments/assets/001a9604-ce62-4369-9ba3-cbb1a87aa34d" alt="test7">
                    <img class="test-thumb" src="https://github.com/user-attachments/assets/f52862c4-33b8-4ca8-9f24-6de199d26fcc" alt="test8">
                    <img class="test-thumb" src="https://github.com/user-attachments/assets/c7ebe7f7-cf5e-4a3e-9a45-3cf4758d7477" alt="test9">
                    <img class="test-thumb" src="https://github.com/user-attachments/assets/c1ed33b4-0177-4514-ba9d-92d20751953e" alt="test10">
                    <img class="test-thumb" src="https://github.com/user-attachments/assets/90e8e7af-0342-4060-bd7e-a59596b87952" alt="test11">
                    <img class="test-thumb" src="https://github.com/user-attachments/assets/5257826b-a037-4ec0-933e-5c6609d76be8" alt="test12">
                </div>
                <div style="font-size:0.7rem; margin-top:6px; text-align:center;">↑ inference samples (real-time classification results)</div>
            </div>

            <hr>
            <div class="reflection-text">
                <strong>💡 Reflection Q&A</strong><br><br>
                <strong>1. Images per class & accuracy:</strong> More images improved accuracy (richer feature extraction); rare misclassifications for underrepresented species.<br><br>
                <strong>2. Commonly misclassified:</strong> Similar leaf texture bamboos (Bambusa vs. Phyllostachys) & species with analogous growth habits; fine-grained visual distinctions remain challenging.<br><br>
                <strong>3. Hyperparameters effect:</strong> More epochs → higher training accuracy but risk of overfitting (validation loss plateau). Batch size 32 stable; learning rate 0.001 gave steady convergence.<br><br>
                <strong>4. Dataset challenges:</strong> Varied lighting, background, duplicate images; labeling required careful botanical validation to avoid genus confusion.<br><br>
                <strong>5. Improvements:</strong> Add more field images + data augmentation (rotation, color jitter). Use attention mechanism, fine-tune CNN backbone, and expand rare species samples.
            </div>
            <div style="margin-top: 1rem; font-size:0.75rem; background:#eaf3e3; border-radius: 1rem; padding:0.4rem 0.8rem; text-align:center;">
                🧠 Model architecture: EfficientNet-B0 • Transfer learning • Training accuracy 94%, Val accuracy 92.4%
            </div>
        </div>
    </div>
    <footer>
        🌱 Plant-Species-Image-Classification • Bamboo dataset • Organized in responsive columns & rows • Scientific descriptions + visual benchmarks
    </footer>
</div>
</body>
</html>
```
