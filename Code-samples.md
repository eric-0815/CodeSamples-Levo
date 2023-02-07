# Code Samples


## Bad Samples

#### FrontEnd

```js
//Here's a sample for rendering all the tasks, which should be sorted by their points when displayed using React.
// Each task has a "point" property that determines its priority.
 export default class App extends Component {
  state = Object.assign(
    {
      newTask: "",
      tasks: [],
    },
    this.props.initialState
  );
  handleSubmit = (event) => {
    event.preventDefault();
    const valueNum = Number(this.state.newTask.replace(/[^0-9]/gi, ""));
    const newTasks = [
      ...this.state.tasks,
      { name: this.state.newTask, points: valueNum },
    ].sort((a, b) => b.points - a.points);
    this.setState({ tasks: newTasks, newTask: "" });
  };
   render() {
    return (
      <div className="App">
            <List component="nav">
              {this.state.tasks.map((task, i) => (
                <div
                  key={i}
                  className={task.points >= 10 ? "critical" : "normal"}
                >
                  <ListItem button>
                    {!this.state.isOpen && <ListItemText
                      primary={task.name}/>}
                  </ListItem>
                </div>
              ))}
            </List>
      </div>
    );
  }
}

```

#### Backend

```ts
// Here's a sample for creating an API for template display, which should be paginated and filterable for display in various areas.

async getAllTemplates(
    getAllTemplates: GetAllTemplatesDto,
  ): Promise<TemplateItem[]> {
    const { user_id, limit = 0, offset = 0, filterTag } = getAllTemplates;
    const optionalQuery: { [key: string]: any } = {};
    const courts = COURT_LISTS;  // we totally have six kinds of basketball courts

    if (user_id) optionalQuery.user_id = user_id;
    if (filterTag) optionalQuery.filterTag = filterTag;

// Optimize logic to reduce duplicated codes
    if (user_id) {
        const templates = await this.TemplateModel.find({
            isDeleted: false,
            ...optionalQuery,
            "tags.CourtCategory": optionalQuery.filterTag ? optionalQuery.filterTag : courts,
          })
            .sort({ createdAt: -1 })
            .skip(offset)
            .limit(limit)
            .exec();   
          return templates;  // all templates can be displayed.
        } else {
            const templates = await this.TemplateModel.find({
                isDeleted: false,
                ...optionalQuery,
                "tags.CourtCategory": optionalQuery.filterTag ? optionalQuery.filterTag : courts,
                status: "published",   // only published templates can be displayed.
              })
                .sort({ createdAt: -1 })
                .skip(offset)
                .limit(limit)
                .exec();
        
              return templates;
            }
          }
```

## Good examples

#### Front end

```tsx
// here is an example I need to transfer our 2D court to 3D by using Ts,Chakra UI, redux toolkit
interface Props {
  width: number;
  height: number;
  children: ReactNode;
}

const ThreeDimensionalToggle = ({ width, height, children }: Props) => {
  const dispatch = useDispatch();
  const { isSwitch3D } = useStoreSelector((state) => state.buttonToggle);
  const { onClose } = useDisclosure();
  const handleOpenSwitch3D = async () => {
    await dispatch(resetAll());
    dispatch(switch3D(true));
    dispatch(changeSelectedColor("none"));
  };
  const handleClose3D = () => {
    onClose();
    dispatch(switch3D(false));
  };
  return (
    <>
      <Flex
        onClick={handleOpenSwitch3D}
        cursor="pointer"
        zIndex={10}
      >
        <Icon as={IoCubeSharp} width={6} height={6} />
        <Text fontSize="12px">3D Preview</Text>
      </Flex>
      <ThreeDimensionalContainer
        isOpen={isSwitch3D}
        onClose={handleClose3D}
        width={width}
        height={height}
        content={children}
      />
    </>
  );
};

export default ThreeDimensionalToggle;


```
```ts

// Here's a sample for writing a function to search the tax amount people should pay based on the tax table.
const TAX_TABLE_2022 = [
  { min: 0, max: 18200, accumulate: 0, rate: 0 },
  { min: 18200, max: 37000, accumulate: 0, rate: 0.19 },
  { min: 37000, max: 90000, accumulate: 3572, rate: 0.325 },
  { min: 90000, max: 120000, accumulate: 20797, rate: 0.37 },
  { min: 120000, max: 180000, accumulate: 22311, rate: 0.39 },
  { min: 180000, max: Number.POSITIVE_INFINITY, accumulate: 54097, rate: 0.45 },
];

const calculateTax = (salary, taxTable)  => {
  const result = taxTable.find((row) => salary > row.min && salary < row.max);
  const { accumulate, rate, min } = result;
  const tax  = (salary - min) * rate + accumulate;

  return tax;
}


```

#### Backend
```ts
// Here is the update example for creating an API for template display, which should be paginated and filterable for display in various areas.
  async getAllTemplates(
    getAllTemplates: PaginationQueryDto & GetAllTemplatesDto,  //Divide DTO into pagination and getAll 
  ): Promise<TemplateItem[]> {
    const { user_id, limit = 0, offset = 0, filterTag, status = "published" } = getAllTemplates;
    const optionalQuery: { [key: string]: any } = {};

    if (status !== "all") {
      optionalQuery.status = status;
    } else {
      optionalQuery.status = ["published", "private", "censoring", "illegal"];
    }

    if (filterTag) optionalQuery["tags.CourtCategory"] = filterTag;
    if (user_id) {
      optionalQuery.user_id = user_id;
      optionalQuery.status = { $in: ["published", "private", "censoring"] };
    }

    const templates = await this.TemplateModel.find({
      isDeleted: false,
      ...optionalQuery,
    })
      .sort({ createdAt: -1 })
      .skip(offset)
      .limit(limit)
      .exec();
    return templates;
  }
```
